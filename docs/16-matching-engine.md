# 交易所撮合系统：订单簿、架构与开源实现

撮合引擎（matching engine）接收并排序订单，在规则允许时将买卖订单撮合成成交。它是交易系统的核心部件之一，但不等同于完整交易所：接入网关、账户与风控、资金账本、行情发布、清算结算、资产托管和运营监控通常由周边系统共同完成。

本专题主要讲中心化交易场所的连续限价订单簿（CLOB），并以 dYdX Chain 说明链上衍生品订单簿的差异。不同市场的订单优先级和交易规则由交易场所具体定义；以下流程是常见架构模型，不是任何一家交易所的完整内部设计披露。

## 一、订单簿与基本撮合规则

一个交易对的订单簿通常分为买盘（bids）和卖盘（asks）。每侧按价格组织价位，同一价位再保存等待成交的订单队列。限价买单的价格达到或高于最低卖价时可成交；限价卖单的价格达到或低于最高买价时可成交。

常见的**价格—时间优先（price-time priority）**规则是先选择价格更优的挂单；同一价格下，再按交易场所定义的接收/排队次序处理。Nasdaq 的规则还区分显示与非显示数量，并对部分订单类型和改价行为规定特定排序，因此“价格—时间优先”不是所有市场规则的完整描述。[Nasdaq 股票市场规则与订单功能说明](https://nasdaqtrader.com/Trader.aspx?id=TradingUSEquities)；[Nasdaq Rulebook](https://listingcenter.nasdaq.com/rulebook/nasdaq/rules/Nasdaq%20Equity%204)。CME Globex 则为不同产品配置 FIFO、Pro Rata、TOP、LMM 等组合算法，可参阅 [CME 匹配算法资料](https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457316046/)。这些是传统金融市场案例，可帮助理解“撮合规则属于市场制度的一部分”，不应直接当成所有加密现货/合约市场的规则。

常见订单属性包括：

- **Market / Limit**：市价单以可成交为目标，限价单不得以差于限价的价格成交；未成交的限价单是否进入簿内取决于订单属性。
- **GTC / IOC / FOK**：分别控制有效期、立即成交后取消剩余数量，以及必须一次全部成交否则取消。不同 venue 对 FOK 和市价单等细节可能有差异。
- **Post-only / Reduce-only**：前者通常用于避免成为 taker，后者用于限制衍生品订单只减少已有仓位；执行时需根据市场和风险状态定义拒单或改单行为。
- **取消、改单、自成交保护**：改单是否保留原队列优先级、跨账户自成交时取消哪一边，都会影响公平性和撮合结果，必须被明确写入规则并可重放。

连续撮合的典型过程：新订单先经过参数、余额/保证金和限额检查；随后与对手盘按规则成交；部分成交后将剩余数量入簿或取消；每次状态变化产生确定的成交与订单事件，并返回给用户和行情订阅者。常见连续限价簿通常以被动挂单价格作为成交价格，但具体成交价格规则仍应以对应 venue 的规则为准。

## 二、从 API 到成交回报：常见系统边界

```text
FIX / REST / WebSocket Gateway
          ↓ 认证、限流、协议校验、订单归一化
预交易风控与资金/保证金预留
          ↓ 按市场/交易品种排序并分发
确定性撮合状态机 ←→ 内存订单簿
          ↓ 成交、撤单、拒单、簿更新事件
持久化日志/快照 · 用户回报 · 行情发布 · 账本/清算
```

要点在于职责隔离：

1. **网关不负责最终排序**：多个客户端连接和网关会并发接收请求。市场规则需要一个权威的序列化点，为影响同一订单簿的命令确定唯一先后顺序。
2. **风控与资金状态一致**：接单前校验账户状态、余额/保证金、价格带、仓位和频率限额；挂单时需要预留相应资源，成交/撤单后再按确定的事件更新账本。撮合成交与链上/银行结算不是同一件事。
3. **撮合核心只处理已排序的命令**：对单一订单簿按确定顺序执行，产生明确的成交和簿变更；对多个互不相关的市场，可按 symbol/market 分片并行。
4. **行情和用户回报是下游投影**：它们消费权威事件，生成 L2 深度、逐笔成交、订单状态等视图。行情接口可能有聚合或传输延迟，不应当被当作撮合核心的权威状态。

Coinbase 与 AWS 的架构分享把交易系统描述为低延迟、单线程且确定性的撮合服务，并展示订单管理系统、撮合引擎、网关和行情接口的拆分，以及通过 Raft/Aeron 进行集群复制的设计。它是特定系统的工程分享，而非所有交易所的标准答案：[Building an ultra-low-latency crypto exchange on AWS（AWS re:Invent 2023）](https://d1.awsstatic.com/events/Summits/reinvent2023/FSI309_Coinbase-Building-an-ultra-low-latency-crypto-exchange-on-AWS.pdf)。

## 三、关键实现思想与工程取舍

### 1. 确定性排序与单写者

对于同一本订单簿，同一时刻只能有一个有效的命令顺序。常见设计是每个市场使用一个 sequencer 或确定性处理队列，由单个执行线程独占更新该簿；网关、行情分发、风控计算等外围工作可并行处理。这样可减少共享可变状态、锁竞争和同价订单的排序歧义。LMAX 对 [Disruptor 的设计说明](https://github.com/LMAX-Exchange/disruptor/blob/master/src/docs/asciidoc/en/disruptor.adoc)阐述了 ring buffer、生产者/消费者和 single-writer 思路。

单写者并不代表系统只用一个线程或只有一台服务器。外围和不同市场可以并发；对单个 symbol 如何拆分写路径则必须避免破坏顺序。复制节点收到相同输入后，撮合逻辑、整数运算、时间戳来源和排序规则都应产生相同结果。

### 2. 数据结构与整数定点数

订单簿常用价格档索引和档内 FIFO 队列：价格侧可由有序树、跳表、堆加索引或适用于价格范围的数组维护；每档队列需要支持头部撮合、撤单和通过 order ID 快速定位。数据结构应根据价格档密度、订单量、撤单率和缓存局部性基准测试，而不是只比较理论复杂度。

价格和数量应按 tick size、lot size 转换成整数刻度（fixed-point / integer units）保存，避免二进制浮点误差造成余额、费率或成交数量的不一致。边界需要明确处理精度、溢出、舍入方向和最小下单量。

### 3. 事件日志、快照与恢复

将被接受的命令按确定顺序写入持久化日志（WAL/journal），定期保存订单簿及账户相关状态快照；进程恢复时加载快照并按顺序重放后续事件，得到可核对的状态。ACK 在日志何时落盘、日志复制要等几份、快照如何校验，会影响延迟和故障恢复目标，需明确设计。

客户端重试、网络超时和主备切换可能重复提交同一请求。幂等请求 ID、严格递增序号、订单生命周期状态机、成交去重和主节点 fencing 能帮助避免重复成交或双主写入。应验证恢复后的订单簿、余额、成交总量和行情序号相互一致。

### 4. 风控、过载与公平性

吞吐量之外还需要关注 tail latency（如 p99/p999）、订单拒绝率、队列积压、丢包恢复和行情延迟。过载时，限流、背压、熔断、价格保护和降级路径要写清楚，不能仅靠无限缓冲队列拖延故障。

接收时间如何定义会影响排队公平性：若不同网关自行打时间戳再竞争入簿，时钟差和网络路径可能造成不透明排序。最好将交易场所实际采用的优先级标准、时戳/序号来源、改单优先级、撮合算法及异常处理公开记录。加密市场还需防止重复订单、撤单竞态、自成交和仓位检查竞态。

## 四、中心化引擎与链上/共识复制订单簿

中心化 CEX 通常由交易场所控制唯一权威撮合状态，并用复制、日志和灾备方案提高可用性。链上订单簿则必须考虑共识：各验证者/节点如何对订单输入和成交结果达成一致、哪些订单会进入区块、链重组/排序延迟以及区块提议者能获得何种排序影响。

[dYdX Chain 的开源代码](https://github.com/dydxprotocol/v4-chain)是可读的链上衍生品案例：协议源码包含 CLOB 模块、价格档和同档订单队列等结构（参见 [`orderbook.go`](https://github.com/dydxprotocol/v4-chain/blob/main/protocol/x/clob/types/orderbook.go)），也包含订单撮合、账户抵押检查和区块操作提议逻辑。它不是简单把传统 CEX 单线程引擎搬上链；要结合其 Cosmos SDK/CometBFT 共识、短期订单和链上状态更新路径理解。研究 dYdX 可以帮助比较 CEX 与共识系统，但不能据此假设其他 DEX 有相同排序或 MEV 风险模型。

## 五、可读的论文、技术材料和开源项目

| 资源 | 类型 | 值得看的内容 | 使用边界 |
|---|---|---|---|
| [Coinbase/AWS：低延迟加密交易所架构分享](https://d1.awsstatic.com/events/Summits/reinvent2023/FSI309_Coinbase-Building-an-ultra-low-latency-crypto-exchange-on-AWS.pdf) | 交易所工程架构分享 | OMS、matching engine、网关、行情、单线程确定性核心、Raft/Aeron 复制和延迟/韧性取舍。 | 2023 年的会议资料；展示的是特定架构，不代表 Coinbase 当前全部实现或行业统一方案。 |
| [LMAX Disruptor 论文/设计说明](https://github.com/LMAX-Exchange/disruptor/blob/master/src/docs/asciidoc/en/disruptor.adoc) · [项目主页](https://lmax-exchange.github.io/disruptor/) | 并发与消息传递技术 | Ring buffer、事件处理依赖、单写者原则、低锁竞争设计。 | Disruptor 是消息传递库，不是订单簿、风控系统或完整撮合引擎。性能数字依赖硬件和测试方法。 |
| [CoinTossX 论文](https://www.sciencedirect.com/science/article/pii/S2352711022000875) · [源代码](https://github.com/dharmeshsing/CoinTossX) | 学术论文与模拟撮合项目 | 论文描述 Java、SBE、Aeron/UDP、市场数据网关及模拟客户端；适合追踪组件边界和运行方式。 | 以 JSE 规则为基础；仓库要求 Java 8，属于研究/教学参考。检查依赖和代码维护状态，不要把论文中的测试环境性能直接当生产承诺。 |
| [exchange-core](https://github.com/exchange-core/exchange-core) | Java 撮合引擎库 | 内存订单簿、账户风控、journal/replay、快照、定点数、Disruptor 多阶段处理和一致性测试入口。 | README 中的微秒级数据为项目自报结果；仓库 TODO 仍列出行情、清算、集群、FIX/REST 网关等缺口。适合学习核心实现，不是完整交易所产品。 |
| [dYdX Chain v4](https://github.com/dydxprotocol/v4-chain) | 共识链上的衍生品协议 | Go/Cosmos SDK/CometBFT、CLOB 状态、订单验证和匹配操作，可研究共识与撮合的结合。 | 需要理解协议版本、短期/长期订单和链上治理；不同于传统 CEX 的内部引擎。 |

### 技术博客与系统学习文章

| 文章 | 适合了解 | 阅读时注意 |
|---|---|---|
| [〖金融科技工程〗撮合引擎实现：撮合算法、价格优先时间优先、状态机、低延迟工程](https://quant67.com/post/fintech/16-matching-engine/16-matching-engine.html)（中文） | 一篇长文覆盖订单簿结构、价格档与 FIFO、确定性/序列号、订单状态机、Go/Rust 示例、事件回放、风控协同、撤单、监控和压测；文末列出 Nasdaq、CME、LMAX、dYdX 等参考资料。 | 是个人技术博客，不是交易所的内部设计披露。其“主流交易所普遍如何实现”等概括和具体参数建议应当作为作者观点，再用官方规则、源码或论文验证。 |
| [永续合约 09：撮合引擎原理与 Go 实现](https://mritd.com/2025/11/08/perp-matching-engine/)（中文） | 从树/B-Tree/跳表选型开始，给出 Go 的价格—时间优先实现，再讨论分片、队列、事件溯源及 DEX 场景；属于永续合约系列中的撮合专题。 | 很适合跟着代码学习核心算法；Snowflake、机器 ID、无锁扩容等方案是设计讨论，需结合实际排序语义、故障模型和测量结果评估。 |
| [Building a High-Performance Order Book from Scratch in C++](https://medium.com/@athangkali21/building-a-high-performance-order-book-from-scratch-in-c-0b424efae3f2)（英文，多篇系列） | 路线图从订单簿、价格档和 FIFO，逐步做到限价/市价、撮合、撤改单、L1/L2/L3 行情与性能改进，适合作为边读边写的入门练习。 | 作者个人教程，不代表生产交易所架构；系列仍应以实际已发布文章和仓库代码为准。 |
| [A journey to build a Microservice Crypto exchange](https://medium.com/@rico.zhang/build-a-microservice-crypto-exchange-in-3-months-92f49f8b7618)（英文，2018） | 一线项目经验角度讨论 RPC 服务、内存撮合、Kafka 输入/输出、重启恢复、重复投递、最终一致性和精度问题。 | 年份较早且是作者对单个项目的复盘；适合读故障和边界经验，不宜把其技术栈或架构当成当前通用最佳实践。 |
| [Internal Racing Conditions in Crypto Exchanges](https://medium.com/open-crypto-market-data-initiative/internal-racing-conditions-in-crypto-exchanges-cac782f77fd8)（英文） | Open Crypto Trading Initiative 通过下单、撤单与余额复用实验讨论撮合回报和风控余额更新之间的异步竞态，适合补充 API 与用户观察到的系统一致性问题。 | 文章报告的是特定时期、特定交易所 API 的实验观察，不能推断所有交易所都有相同缺陷，也不是撮合引擎完整实现教程。 |

微信公众号检索方面，本次没有找到同时具备连续系统讲解、实现细节和可交叉核验出处的公众号系列。中文博客和公开源码更容易核实；遇到只宣传“源码搭建交易所”、不说明撮合规则、恢复流程、代码许可或压测方法的文章/项目，建议谨慎看待。

### 建议阅读顺序

1. 先读 Binance Academy 的[撮合引擎入门](https://www.binance.com/en/academy/glossary/matching-engine)，再对照 Nasdaq/CME 规则，分清常见概念和具体 venue 的规则。
2. 阅读 quant67 长文建立总体框架；再跟 mritd 或 Athang Kali 系列做小型单市场订单簿实现，自己验证部分成交、FIFO、撤单、改单和拒单边界。
3. 阅读 Coinbase/AWS 架构图，画出从订单网关到成交事件、用户回报、行情和账本的边界。
4. 阅读 LMAX Disruptor 材料理解事件流水线，再看 exchange-core 的 order book、matching、journal 和 snapshot 代码。
5. 阅读 CoinTossX 论文并本地运行，理解模拟客户端与撮合服务如何通过消息协议交互。
6. 最后阅读 dYdX CLOB 源码，对照共识、状态机和排序约束，分析其与中心化订单簿的差异。

做性能对比时应同机、同数据集、同订单类型分布和同正确性要求，分别报告吞吐、p50/p99/p999 延迟、重放能力和过载表现。只看 README 中的“orders per second”数字容易忽略订单簿深度、撤单占比、持久化和网络路径等关键差别。

> 本专题用于系统设计和源码学习。订单撮合涉及资产与市场公平，生产环境还必须评估安全审计、资金账本一致性、合规要求、灾备演练和运营流程；“能撮合”不等于“能安全运行交易所”。

*最后核对：2026-10-12。*
