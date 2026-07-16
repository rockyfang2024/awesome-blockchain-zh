# Master Blockchain · 精通区块链

> 🎯 **目标**：成为 GitHub 上学习区块链最全的中文资源仓库。
> 涵盖 Ethereum / Solana / BTC 等主流 L1/L2，从入门到精通的全套资源 + 知识笔记。

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

---

## 🏆 这个仓库提供什么

### 📚 完整的学习路径

- **零基础入门**：什么是区块链、公链、私钥、Gas、DeFi/NFT/DAO
- **按公链分**：Bitcoin / Ethereum / Solana / Aptos / Sui 等
- **按方向分**：智能合约、DeFi 协议、安全审计、底层原理

### 🔥 热点事件分析（本仓库特色）

每次区块链行业发生重大事件（被盗、暴雷、黑客攻击），我们做深度复盘，提取开发者/用户/协议设计者的学习点。

- Bybit 冷钱包被盗（$15 亿）
- FTX 暴雷（$80 亿缺口）
- WazirX、DMM Bitcoin、Penpie 等

> 其他 awesome 仓库**几乎不做事件分析** —— 这块是我们独有的深度内容。

### 🎬 视频教程

- 中文（B 站）：Solidity / Web3 全栈 / DeFi / Solana
- 英文（YouTube）：Patrick Collins、Nader Dabit 等
- 在线交互：CryptoZombies / Speed Run Ethereum / Solana Playground

### 💻 推荐开源项目

按语言分类（Go / Rust / Solidity），每个项目标注"学什么"：
- BTC / ETH / Solana 节点源码
- OpenZeppelin 合约库
- Uniswap V3、Aave、Compound 等 DeFi 协议实现

### 📰 信息源（其他仓库多缺失）

- 中文公众号 / Newsletter
- Twitter / X 必关注
- 链上数据平台（Glassnode / Dune / DefiLlama）

### 🇨🇳 中文社区

- 中文论坛 / Discord / 媒体（链得得 / PANews / 深潮 TechFlow）

### 📅 持续维护

- 每个资源**标注最后验证日期**
- 公链对比表 / L2 类型表 / 协议分类表都按**当下行业现状**更新
- PR 流程清晰，新事件分析有模板

---

## ⚠️ 数据时效性

本仓库所有数据（事件、链接、价格、TVL）都可能快速变化。任何具体数字请以原始来源为准。
本仓库**只做学习资源的整理和事件的分析框架**，不提供投资建议。

---

## 🚀 快速导航

| 我是... | 我想... | 推荐入口 |
|---------|---------|----------|
| 完全新手 | 了解区块链是什么 | [📘 区块链入门 101](#-区块链入门-101-零基础) |
| 想学 Solidity | 写智能合约 | [🛠️ Solidity 学习路径](#-solidity-智能合约) |
| 学 Solana | 写 Rust 合约 | [☀️ Solana / Rust 学习路径](#-solana--rust-生态) |
| 学 BTC 原理 | 理解底层 | [₿ Bitcoin 学习路径](#-bitcoin-底层) |
| 想找视频课 | B 站 / YouTube | [🎬 视频教程合集](#-视频教程) |
| 想看书 | 区块链书籍推荐 | [📚 必读书单](#-必读书单) |
| 想做项目 | 看开源项目 | [💻 推荐项目](#-推荐开源项目) |
| 想跟前沿 | 公众号 / newsletter | [📰 信息源](#-信息源) |
| 准备面试 | Solidity 面试题 | [docs/solidity-interview.md](docs/solidity-interview.md) |

---

## 📘 区块链入门 101（零基础）

> 这一章写给完全没接触过区块链的人。建议顺序阅读。

### 1. 什么是区块链

- **本质**：去中心化的分布式账本
- **关键概念**：区块、链、哈希、共识机制、矿工/验证者
- 推荐先看：[📖 推荐链接占位] —— 待补充权威科普文章

### 2. 公链 vs 私链 vs 联盟链

- **公链（Public）**：完全开放，任何人可读写 —— BTC / ETH / Solana
- **联盟链（Consortium）**：部分节点验证 —— Hyperledger Fabric
- **私链（Private）**：单一组织内部 —— 企业内部账本

### 3. 钱包、私钥、地址

- **私钥 = 银行卡密码 + 身份证**（不能丢，不能告诉别人）
- **地址 = 银行卡号**（可以公开）
- **助记词 = 私钥的备份形式**（12/24 个英文单词）

### 4. Gas / 交易 / 区块

- **Gas**：你为链上操作付的"燃料费"
- **交易（Tx）**：你在链上做的任何操作（转账、调用合约）
- **区块（Block）**：一批交易打包的结果，约每 12 秒（ETH）/ 400ms（Solana）出一个

### 5. DeFi / NFT / DAO / 稳定币

| 概念 | 一句话 | 代表项目 |
|------|--------|----------|
| DeFi | 去中心化金融（不靠银行） | Uniswap / Aave / Compound |
| NFT | 链上唯一资产凭证 | OpenSea / Blur |
| DAO | 去中心化自治组织 | MakerDAO |
| 稳定币 | 锚定法币的代币 | USDT / USDC / DAI |

---

## 🛠️ Solidity 智能合约

### 学习路径（推荐顺序）

1. **入门**：Solidity 官方文档 / CryptoZombies
2. **基础**：Hardhat / Foundry 写 Hello World
3. **进阶**：OpenZeppelin 合约库（ERC20/ERC721 实现）
4. **深入**：EVM 底层 / Gas 优化 / 安全审计

### 推荐资源

- 📖 [Solidity 官方文档（中文）](https://docs.soliditylang.org/zh/latest/) — 权威但偏难
- 🌐 [CryptoZombies](https://cryptozombies.io/zh/) — 边玩边学，最适合入门
- 📖 [Solidity by Example](https://solidity-by-example.org/) — 看代码学语法
- 🛠️ [Hardhat 官方文档](https://hardhat.org/docs) — 主流开发框架
- 🛠️ [Foundry Book](https://book.getfoundry.sh/) — 更快的 Solidity 工具链
- 📚 [OpenZeppelin 合约库](https://docs.openzeppelin.com/contracts) — 工业级合约实现

### 知识笔记（本仓库内）

- 📄 [Solidity 开发环境搭建（VSCode + Hardhat）](2025-08-03-vscode-hardhat搭建solidity开发环境.md)
- 📄 [合约开发相关术语](2025-08-05-合约开发相关术语.md)

---

## ☀️ Solana / Rust 生态

### 为什么学 Solana

- **高性能**：理论 65,000 TPS，目前实测 3,000+ TPS
- **低费用**：单笔交易约 $0.00025
- **Rust 语言**：比 Solidity 难学，但更接近底层、性能更好

### 学习路径

1. **Rust 基础**：The Rust Book（强烈推荐）
2. **Solana 基础**：Solana Cookbook 中文版
3. **Anchor 框架**：Solana 上的"Hardhat"
4. **实战项目**：写 SPL Token / AMM

### 推荐资源

- 📖 [The Rust Programming Language（中文）](https://rustwiki.org/zh-CN/book/) — Rust 圣经
- 📖 [Solana Cookbook（中文）](https://solanacookbook.com/zh/) — 官方推荐教程
- 🛠️ [Anchor 文档](https://www.anchor-lang.com/docs) — Solana 主流开发框架
- 🎬 [Solana 大使课程（B 站）](https://www.bilibili.com) — 待补充具体链接

---

## ₿ Bitcoin 底层

### 为什么学 BTC

- 最老、最稳、共识最强的公链
- 理解 BTC 才能理解所有"模仿者"
- 闪电网络、Ordinals、Stacks 等生态都在扩展 BTC

### 学习路径

1. **白皮书**：中本聪《Bitcoin: A Peer-to-Peer Electronic Cash System》（仅 9 页）
2. **Mastering Bitcoin**（Andreas Antonopoulos 著）
3. **BIP 流程**：理解 BTC 的提案机制
4. **源码**：[bitcoin/bitcoin](https://github.com/bitcoin/bitcoin) C++ 实现

### 推荐资源

- 📖 [Bitcoin 白皮书（中文）](https://bitcoin.org/files/bitcoin-paper/bitcoin_zh_cn.pdf) — 必读
- 📖 [Mastering Bitcoin（中文译本）](https://www.btcstudy.org/) — BTCstudy 翻译版
- 🔗 [Learn Me a Bitcoin](https://learnmeabitcoin.com/) — 图解 BTC 原理

---

## 🌐 L1 / L2 公链生态

### 主流公链一览

| 公链 | 共识 | 编程语言 | TPS 量级 | 主打特点 |
|------|------|----------|----------|----------|
| **Bitcoin** | PoW | Script | ~7 | 数字黄金 |
| **Ethereum** | PoS | Solidity | ~30 | 智能合约之王 |
| **Solana** | PoH + PoS | Rust | ~3,000 | 高性能 |
| **BNB Chain** | PoSA | Solidity | ~300 | 币安生态 |
| **Avalanche** | Snowman | Solidity | ~4,500 | 子网定制 |
| **Polygon** | PoS | Solidity | ~7,000 | 以太坊侧链 |
| **Cosmos** | Tendermint | Go / CosmWasm (Rust) | 取决于链 | 应用链 |
| **Polkadot** | NPoS | Rust (Substrate) | ~1,000 | 跨链 |
| **NEAR** | Doomslug | Rust / AssemblyScript | ~1,000 | 分片 |

### Layer 2 扩容方案

| 类型 | 代表项目 | 原理 |
|------|----------|------|
| **Optimistic Rollup** | Optimism / Arbitrum | 假设交易有效，7 天挑战期 |
| **ZK Rollup** | zkSync / Starknet | 用零知识证明验证交易 |
| **State Channel** | Lightning（BTC） | 链下多次交易，链上最终结算 |
| **Sidechain** | Polygon PoS | 独立共识，桥接主链 |
| **Plasma** | 已淘汰 | 历史方案 |

---

## 🎬 视频教程

### 中文（B 站为主）

| 课程 | 适合 | 链接 |
|------|------|------|
| Solidity 入门到精通 | 初学者 | 占位：待补充 |
| Web3 全栈开发 | 想做 dApp 的全栈工程师 | 占位 |
| DeFi 协议剖析 | 中级 | 占位 |
| Solana 中文教程 | 学 Rust 的 | 占位 |
| 区块链底层原理 | 想理解底层 | 占位 |

### 英文（YouTube / 免费课）

| 课程 | 适合 | 链接 |
|------|------|------|
| [Patrick Collins](https://www.youtube.com/@PatrickCollins) Solidity | 入门 - 进阶 | YouTube |
| [Nader Dabit](https://www.youtube.com/@naderdabit) 全栈 Web3 | 中级 | YouTube |
| [Web3 University](https://www.web3.university/) | 实战项目 | 网站 |
| [Eat the Blocks](https://www.youtube.com/@eattheblocks) | DeFi 深入 | YouTube |

### 在线交互教程

- 🌐 [CryptoZombies](https://cryptozombies.io/zh/) — 边玩边学 Solidity
- 🌐 [Speed Run Ethereum](https://speedrunethereum.com/) — Scaffold-ETH 实战
- 🌐 [Solana Playground](https://beta.solpg.io/) — 浏览器里写 Solana
- 🌐 [Remix IDE](https://remix.ethereum.org/) — 在线 Solidity 编辑器

---

## 📚 必读书单

### 中文入门

| 书名 | 作者 | 适合 |
|------|------|------|
| 《区块链：从数字货币到信用社会》 | 长铗 / 韩锋 | 零基础科普 |
| 《比特币：一个虚幻而真实的金融未来》 | 李钧 / 长铗 | BTC 入门 |
| 《以太坊技术详解与实战》 | 汪晓明 | Solidity 入门 |

### 英文进阶

| 书名 | 作者 | 适合 |
|------|------|------|
| **Mastering Bitcoin** | Andreas Antonopoulos | BTC 圣经（中文译本有） |
| **Mastering Ethereum** | Andreas Antonopoulos | ETH 圣经 |
| **Solidity Programming Essentials** | Ritesh Modi | Solidity 入门 |
| **Hands-On Smart Contract Development with Solidity and Ethereum** | Kevin Solorio | 实战 |
| **Building Secure & Reliable Systems** | Google SRE 团队 | 不区块链但讲分布式系统设计 |

### 论文（理解底层原理）

- 中本聪《Bitcoin: A Peer-to-Peer Electronic Cash System》
- Vitalik《Ethereum White Paper》
- Wood《Polkadot: Vision for a Heterogeneous Multi-Chain Framework》

---

## 💻 推荐开源项目

### 想读源码 / 学架构

| 项目 | 语言 | 学什么 |
|------|------|--------|
| [bitcoin/bitcoin](https://github.com/bitcoin/bitcoin) | C++ | BTC 节点实现 |
| [ethereum/go-ethereum](https://github.com/ethereum/go-ethereum) | Go | ETH 客户端 |
| [solana-labs/solana](https://github.com/solana-labs/solana) | Rust | Solana 节点 |
| [OpenZeppelin/openzeppelin-contracts](https://github.com/OpenZeppelin/openzeppelin-contracts) | Solidity | 工业级 Solidity 库 |
| [Uniswap/v3-core](https://github.com/Uniswap/v3-core) | Solidity | AMM 算法实现 |
| [Aave/aave-v3-core](https://github.com/aave/aave-v3-core) | Solidity | 借贷协议 |
| [compound-finance/compound-protocol](https://github.com/compound-finance/compound-protocol) | Solidity | 借贷鼻祖 |
| [chainlink/contracts](https://github.com/smartcontractkit/chainlink) | Solidity | 预言机 |
| [foundry-rs/foundry](https://github.com/foundry-rs/foundry) | Rust | Solidity 工具链 |

### 想做项目 / Hackathon 参考

- Scaffold-ETH — 全栈 dApp 脚手架
- create-next-dapp — Next.js + Web3 模板
- Solana dApp Scaffold — Anchor + React

---

## 📰 信息源

### 公众号（中文）

| 公众号 | 特点 |
|--------|------|
| 占位：待补充 | - |
| 占位 | - |

### Newsletter / RSS

| 来源 | 特点 |
|------|------|
| [Week in Ethereum News](https://weekinethereumnews.com/) | 每周 ETH 动态 |
| [The Defiant](https://thedefiant.io/) | DeFi 深度报道 |
| [Bankless](https://www.bankless.com/) | 加密原生媒体 |

### Twitter / X 必关注

- @VitalikButerin — ETH 创始人
- @solaboratory — Solana 官方
- @aaboratory — Aave 创始人
- @stableaboratory — stablecoin 领域

### 数据 / 研究

- [Glassnode](https://glassnode.com/) — 链上数据
- [Dune Analytics](https://dune.com/) — 链上查询 SQL
- [DefiLlama](https://defillama.com/) — DeFi TVL 排行
- [Token Terminal](https://tokenterminal.com/) — 协议收入
- [Messari](https://messari.io/) — 研究报告

---

## 🏫 大学公开课

| 课程 | 学校 | 链接 |
|------|------|------|
| Bitcoin and Cryptocurrency Technologies | Princeton | Coursera |
| Blockchain at Berkeley | UC Berkeley | YouTube |
| 区块链与加密货币 | 国内多所 | 占位 |

---

## 🔬 进阶专题

### 密码学基础

- 哈希函数（SHA-256 / Keccak-256）
- 椭圆曲线签名（ECDSA / Ed25519）
- 零知识证明（ZK-SNARK / ZK-STARK）
- BLS 签名聚合

### 共识机制

- PoW（工作量证明）— BTC 早期、ETH 早期
- PoS（权益证明）— ETH 现行
- PoH（历史证明）— Solana
- Tendermint BFT — Cosmos
- HotStuff — Facebook Libra / Aptos

### DeFi 协议剖析

- AMM（Uniswap V2/V3/V4）
- 借贷（Aave / Compound）
- 稳定币（MakerDAO / Curve）
- 衍生品（dYdX / GMX）
- 收益聚合器（Yearn）

### 安全

- 常见漏洞：重入、抢跑、闪电贷攻击
- 审计工具：Slither / Mythril / Echidna
- 审计公司：OpenZeppelin / Trail of Bits / SlowMist

---

## 🇨🇳 中文社区

### 论坛 / Discord

- 占位：待补充

### 媒体

- 链得得（ChinaBanker）
- PANews
- Foresight News
- 深潮 TechFlow

### 活动 / 会议

- 占位：国内 meetup / 黑客松信息源

---

## 🔥 热点事件分析

> **这是本仓库的特色章节**：每次区块链行业发生重大事件（被盗、暴雷、黑客攻击），
> 我们会做一次深度复盘，从事件中提取对开发者 / 用户 / 协议设计者的学习点。
>
> ⚠️ **数据时效性**：事件细节（金额、攻击者、追回情况）可能快速变化。
> 所有数据基于公开报道 + 链上分析，**不代表官方最终结论**。

### 概览（按时间倒序）

| 日期 | 事件 | 类型 | 金额 | 一句话 | 详细 |
|------|------|------|------|--------|------|
| 2025-02-21 | Bybit 冷钱包被盗 | 🔓 exchange_hack | ~$15 亿 | 史上最大加密盗窃之一；Safe{Wallet} 前端攻击 | [→](events/2025/2025-02-21-bybit-hack.md) |
| 2024-07-18 | WazirX 暴雷 | 🔓 exchange_hack | $2.34 亿 | Bybit 之前同类攻击的预演；印度最大交易所 | [→](events/2024/2024-07-18-wazirx-hack.md) |
| 2024-05-31 | DMM Bitcoin 暴雷 | 💥 exchange_collapse | $3.08 亿 | 日本持牌交易所也被盗；SBI VC Trade 接盘 | [→](events/2024/2024-05-31-dmm-bitcoin.md) |
| 2024-01-xx | Penpie 协议攻击 | 🐛 defi_hack | ~$2700 万 | 闪电贷 + 预言机操纵经典案例 | [→](events/2024/2024-01-penpie-hack.md) |
| 2022-11-11 | FTX 暴雷 | 💥 exchange_collapse | $80 亿 | 行业最大丑闻；SBF 判 25 年 | [→](events/2022/2022-11-11-ftx-collapse.md) |

### 按类型分类

| 类型 | 事件 | 共性教训 |
|------|------|----------|
| **exchange_hack** 🔓 | Bybit, WazirX | 冷钱包 + 前端 UI = 攻击面 |
| **exchange_collapse** 💥 | FTX, DMM | 中心化信任的脆弱性 |
| **defi_hack** 🐛 | Penpie | 预言机 + 闪电贷组合攻击 |

### 通用教训（跨所有事件）

| 教训 | 适用对象 |
|------|----------|
| **not your keys, not your coins** | 所有持币者 |
| **多签 + 硬件钱包屏幕核对** | 资金管理者 |
| **POR 不是 100% 证明** | CEX 用户 |
| **预测机用单源 = 自杀** | DeFi 开发者 |
| **前端是攻击面** | Web3 工程师 |
| **大额资产分散持有** | 所有持币者 |

### 事件贡献

如果你想贡献新事件分析，请按以下模板在 `events/YYYY/` 下创建 markdown：

```markdown
# 事件名（YYYY-MM）

> **事件类型**: exchange_hack / exchange_collapse / defi_hack / other
> **金额**: 约 X 亿美元
> **核心问题**: 一句话总结

## 时间线
## 攻击原理 / 问题根源
## 学习要点（分开发者/用户/协议设计者）
## 参考资料
```

---

## 🚧 贡献

欢迎提交 PR 补充资源或修正错误！请确保：

- 资源真实可用（链接能打开）
- 中文资源优先（这是中文资源仓库的定位）
- 简短说明为什么推荐这个资源（一句话即可）
- 按类别放到对应章节

## 📜 License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — 知识共享，署名 + 相同方式共享。

---

> ⭐ 如果这个仓库对你有帮助，请 Star 支持！