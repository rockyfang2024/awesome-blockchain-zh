# 稳定币与底层技术实现

稳定币通常指试图相对某种参考资产（常见为美元）维持较稳定价值的数字资产。“稳定”是设计目标和市场结果，不等于无风险、始终精确等于 1 美元，也不意味着所有持币人都能直接向发行方按面值赎回。链上代币本身只负责记录和转移余额；锚定能否维持，还取决于储备资产、赎回规则、市场流动性、抵押品质量、预言机和治理机制。

## 一、先分清几种机制

| 类型 | 典型例子 | 锚定/稳定机制 | 主要依赖与风险 |
|---|---|---|---|
| 法币或传统资产储备型 | USDC、USDT | 发行方收取法币或符合规则的资产后铸币；合资格客户按发行方条款赎回并销毁代币。储备质量、托管和赎回能力支撑面值锚定。 | 发行方、银行/托管机构、储备透明度、法律权利及赎回门槛；二级市场价格仍会偏离锚定。 |
| 加密资产超额抵押型 | DAI（Maker/Sky 协议） | 用户把波动性加密资产存入 Vault，按抵押率上限生成稳定币；还债后取回抵押品。抵押率不足时，协议出售抵押品清偿债务。 | 抵押品急跌、预言机失灵、清算拥堵或折价、协议治理和坏账风险。 |
| Delta-neutral / 合成美元型 | Ethena USDe | 以现货资产与衍生品空头对冲价格敞口，试图维持美元计价价值；资产托管和交易场所共同参与机制。 | 资金费率和基差、交易所及托管风险、对冲执行、流动性与赎回资格；机制与法币储备型不同。 |
| 算法/弹性供给型 | 设计各异 | 通过算法调整供给、激励或相关代币的兑换关系来影响市场价格。 | 若缺少可兑现的高质量资产与可靠赎回需求，信心下跌可能形成“脱锚—抛售—进一步脱锚”的反馈。不能把算法本身当作储备。 |

Ethereum.org 的[稳定币概览](https://ethereum.org/stablecoins)按法币抵押、加密资产抵押等方式介绍常见设计。比较项目时应看具体的赎回条款和储备，而不是只看名称、链上总供应量或宣传中的“1:1”。

## 二、法币储备型：链上铸币，链下兑付

以美元稳定币为例，典型的发行赎回流程如下：

1. **准入与入金**：用户通常需要通过发行方或合作机构的企业开户、身份核验和制裁筛查；普通用户常在交易所或二级市场买卖，并不一定有直接赎回资格。
2. **铸造（mint）**：发行方确认银行入账及客户资格后，授权链上合约增加供应量，把代币发送到客户指定地址。发行私钥和铸币权限是关键控制面。
3. **流通与转账**：持有人通过链上交易转账，钱包、交易所和 DeFi 协议按相应链上的代币合约读写余额。
4. **赎回与销毁（burn）**：符合条件的客户把代币交回发行方；发行方完成赎回后销毁对应代币并支付法币。实际处理速度、费用、最低金额和资格以合同条款为准。
5. **储备与披露**：发行方管理链下储备并发布储备报告或鉴证材料。链上可以核对特定合约的总供应和转账事件，但不能仅凭链上数据证明银行账户中的储备足额、可及时变现或法律上为代币持有人隔离。

Circle 对[USDC 铸造与赎回](https://www.circle.com/usdc)的说明展示了美元入金后 mint、赎回时 burn 的模式；Circle 的[开源 EVM 稳定币合约](https://github.com/circlefin/stablecoin-evm)还展示了铸币角色、暂停和地址黑名单等发行方控制功能。Tether 的[官方 FAQ](https://tether.to/en/faqs/?only-questions=true&search=How-often-does-Tether-provide-its-transparency-information)说明了多链发行、授权待发行库存、多签授权、销毁及储备披露。以上是发行方资料，阅读时应与服务条款、储备报告及独立监管/审计信息交叉核对。

### ERC-20 合约层

在 Ethereum 上，很多稳定币以 ERC-20 合约形式部署。标准定义了 `totalSupply`、`balanceOf`、`transfer`、`approve`、`transferFrom` 等常用接口及 `Transfer`、`Approval` 事件；它规范代币如何与钱包、交易所和 DeFi 合约交互，不负责证明储备或强制市场价格等于 1 美元。可从 [Ethereum.org 的 ERC-20 文档](https://ethereum.org/developers/docs/standards/tokens/erc-20/)及对应代币的官方合约地址进一步核验。

中心化发行的合约可能在标准转账接口之外加入 `mint`、`burn`、`pause`、`blacklist`、角色权限或升级能力。它们便于合规操作和故障处置，也意味着发行方密钥、角色配置和治理具有实质影响。集成时要核对目标链的**官方合约地址**、代理/实现合约、权限持有人和事件；同名、仿冒或未经授权的“USDC/USDT”并不会因为代币符号相同而成为原生发行资产。

## 三、超额抵押型：Vault、预言机与清算

Sky 协议（MakerDAO 品牌演进后的协议）展示了链上抵押借款式稳定币的一套实现：

1. 用户将受协议接受的抵押品存入 Vault。
2. `Vat` 等会计模块记录抵押品、债务和系统参数；用户在债务上限和最低抵押率约束内生成 DAI。
3. 预言机把抵押品外部市场价格提供给协议；协议可设置延迟/安全模块，以降低错误价格直接生效的风险。
4. 当抵押品价值不足以覆盖债务要求，清算模块将抵押品转入拍卖，出售以回收 DAI 并处理债务和清算罚金。
5. 用户还清债务及费用后，可以取回剩余抵押品。

建议按顺序阅读 [Sky Vault 清算文档](https://developers.skyeco.com/protocol/vaults/collateral-liquidation/)、[安全机制说明](https://developers.skyeco.com/security/security-measures/security-mechanisms/)及其源码链接。文档解释了清算拍卖、价格预言机延迟和债务上限等参数的作用，也指出这些参数本身会带来风险权衡。超额抵押不是“不会脱锚”：极端行情中，抵押品折价出售、链上拥堵、价格源异常或清算流动性不足仍可能产生坏账。

## 四、合成美元：对冲不等于现金储备

Ethena 对 [USDe 机制](https://docs.ethena.fi/)的描述是：协议持有现货资产，同时建立相应衍生品空头头寸，以 delta 对冲减少净价格敞口；资金费率或期货基差变化会影响收益和风险。阅读时不要把它误认为 USDC/USDT 式银行现金储备，也不要把 sUSDe 等收益份额与支付型稳定币混为一谈。应重点检查对冲交易对手、交易所与托管、保证金和清算、资金费率反转、链上赎回限制及协议披露的压力风险。

## 五、跨链：同一符号可能是不同资产

同一个品牌的代币可以有多个链上部署。跨链时至少要分清：

- **发行方原生部署**：发行方在该链直接铸造并承担相应赎回/支持关系。
- **锁定-铸造桥接资产**：源链代币被锁定，桥在目标链铸造包装代币；安全性取决于桥合约、验证者/多签或消息验证机制。
- **销毁-铸造转移**：源链销毁代币，目标链在收到经验证的消息后铸造对应代币。例如 [Circle CCTP](https://www.circle.com/cross-chain-transfer-protocol)为支持的 Circle 资产采用原生 burn-and-mint 流程；这仍依赖协议消息、验证/attestation 和目标链合约正确执行。

桥接包装资产不应仅凭 ticker 当成原生代币。转账前核对资产发行方的支持链列表、官方合约地址、桥接路径和目标网络；错误网络或非官方包装资产可能无法向发行方赎回。Circle 的[支持链列表与入金限制](https://developers.circle.com/circle-mint/supported-chains-and-currencies)也说明了同为 USDC，不同链/跨链路径在 Circle Mint 中可能有不同支持条件。

## 六、锚定如何维持，为什么会脱锚

在有可信直接赎回渠道的情况下，若市场价格显著低于面值，合资格套利者可能买入后赎回；若高于面值，合资格参与者可按规则铸造后卖出。套利需要资金、渠道、结算时间、费用与准入都可用，因此通常只能推动价格靠近锚定，不能保证所有市场、所有时刻恰好等于 1。

可能造成偏离的因素包括储备信用/流动性疑虑、赎回暂停或资格限制、银行或托管中断、做市深度不足、市场恐慌、链上拥堵、抵押品暴跌、预言机或清算问题，以及跨链桥故障。储备披露也有层级差异：代币供应数据、发行方储备构成报告、第三方鉴证和完整财务审计不是同一种证据。

BIS 的[稳定币监管综述](https://www.bis.org/publications/fsi-insight-57-stablecoins-regulatory-responses-their-promise-stability)重点讨论储备、赎回权、资本、治理、网络安全和 AML/CFT 等监管议题；其[2026 年研究](https://www.bis.org/publications/working-paper-1355-making-stablecoins-stabler-can-regulation-help)进一步分析赎回压力、储备流动性和短期国债抛售风险。研究机构分析用于理解系统性风险，不代表任何单一项目的储备审计结论。

## 七、学习与核验清单

阅读或集成一个稳定币时，可依次核查：

1. **机制**：参考资产是什么？实际储备/抵押品是什么？锚定是靠赎回、清算、对冲还是供给调节？
2. **权利**：谁能向发行方直接赎回？有无最低额、费用、地域限制或暂停条件？持币人有无对储备资产的直接法律请求权？
3. **储备**：披露频率与报告类型是什么？资产类别、托管、负债口径和流动性如何？
4. **合约**：官方部署在哪些链？谁持有 minter、pauser、blacklister、升级等权限？是否有审计及已知限制？
5. **预言机与清算**：价格来自哪里、多久更新、异常时如何处理？清算深度和激励是否能覆盖快速下跌？
6. **跨链**：原生部署、发行方支持的迁移协议，还是第三方包装桥？消息验证依赖什么信任假设？
7. **市场**：二级市场流动性、价差和脱锚历史如何？不能把市值、交易量或短期价格稳定当成偿付能力证明。

### 推荐资料

- 入门概览：[Ethereum.org：Stablecoins](https://ethereum.org/stablecoins)
- 代币接口：[Ethereum.org：ERC-20](https://ethereum.org/developers/docs/standards/tokens/erc-20/)
- 发行与代码：[Circle USDC](https://www.circle.com/usdc) · [Circle EVM 合约源码](https://github.com/circlefin/stablecoin-evm) · [Tether FAQ](https://tether.to/en/faqs/?only-questions=true&search=How-often-does-Tether-provide-its-transparency-information)
- 抵押与清算：[Sky Vault 清算](https://developers.skyeco.com/protocol/vaults/collateral-liquidation/) · [Sky 安全机制](https://developers.skyeco.com/security/security-measures/security-mechanisms/)
- 合成美元：[Ethena 文档](https://docs.ethena.fi/)
- 独立政策研究：[BIS FSI Insights 57](https://www.bis.org/publications/fsi-insight-57-stablecoins-regulatory-responses-their-promise-stability) · [BIS Working Paper 1355](https://www.bis.org/publications/working-paper-1355-making-stablecoins-stabler-can-regulation-help)

> 本文介绍公开资料中的常见设计，协议参数和支持的链会变化，请以官方文档与当前合约为准。仅用于学习，不构成购买、交易、收益或托管建议。

*最后核对：2026-10-12。*
