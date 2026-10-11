# 中文区块链开发学习路径

> 面向会编程或正在学编程的中文读者：从理解账本与交易基础，到选择 EVM、Solana、Bitcoin 或 Hyperledger Fabric 方向，再完成一个可运行、可测试的学习项目。这里只收录能支持这条路径的文档、课程、工具和案例。

## 从这里开始

| 阶段 | 入口 | 学完后你应该能 |
|---|---|---|
| 1. 建立基础概念 | [区块链与链上开发入门](docs/01-getting-started.md) | 解释账户、交易、区块、共识、钱包和 RPC 的作用；知道哪些信息需要自己核实 |
| 2. 选择开发方向 | [Solidity / EVM](docs/02-solidity-path.md) · [Solana / Rust](docs/03-solana-path.md) · [Bitcoin](docs/04-bitcoin-path.md) · [Hyperledger Fabric](docs/12-hyperledger-fabric-path.md) | 找到对应的官方文档、工具链和第一份练习 |
| 3. 补齐工程知识 | [进阶专题](docs/10-advanced.md) · [开源项目源码](docs/07-projects.md) | 阅读合约、客户端或协议代码，并理解安全与测试入口 |
| 4. 动手验证 | [交互练习与课程](docs/05-videos.md) | 在本地、浏览器沙盒或测试网完成小型练习；不使用真实资产做学习实验 |
| 5. 从事故学安全 | [事件复盘索引](events/README.md) | 按原始通报和独立技术分析复盘攻击路径、影响与防护边界 |

### 按目标选入口

- **想做 EVM 合约**：先看 [Solidity 学习路径](docs/02-solidity-path.md)，用 Foundry 或 Remix 编译、测试并部署到本地链。
- **想做 Solana 程序**：先过 Rust 基础，再跟随 [Solana 学习路径](docs/03-solana-path.md) 完成官方 Quickstart。
- **想理解 Bitcoin**：从 [Bitcoin 学习路径](docs/04-bitcoin-path.md) 的白皮书、交易结构和 Bitcoin Core 文档开始。
- **做企业联盟链**：从 [Hyperledger Fabric 学习路径](docs/12-hyperledger-fabric-path.md) 开始，重点理解组织身份、通道、背书和客户端 Gateway。
- **开发链上应用**：看 [RPC、钱包与数据索引](docs/13-chain-app-infrastructure.md)，理解合约之外的数据接入、签名与索引边界。
- **想补安全知识**：从 [进阶专题](docs/10-advanced.md) 和 [事件复盘](events/README.md) 开始；复盘结论会区分官方陈述、独立调查和推断。

## 资源目录

| 主题 | 内容 |
|---|---|
| [入门基础](docs/01-getting-started.md) | 核心概念、链上数据与安全基础 |
| [Solidity / EVM](docs/02-solidity-path.md) | 官方语言文档、开发工具和合约练习 |
| [Solana / Rust](docs/03-solana-path.md) | Rust、Solana 官方文档、Anchor 与程序示例 |
| [Bitcoin](docs/04-bitcoin-path.md) | 白皮书、开发者文档、源码和技术通讯 |
| [交互练习与课程](docs/05-videos.md) | 有明确链接的课程、沙盒和安全练习 |
| [书籍与论文](docs/06-books.md) | 基础读物和协议原始资料 |
| [开源项目](docs/07-projects.md) | 按学习目的选择的协议、客户端与工具源码 |
| [信息源](docs/08-info-sources.md) | 官方发布、开发者通讯和链上研究数据 |
| [L1 / L2 参考](docs/09-l1-l2.md) | 架构术语和官方协议文档入口，不做无来源 TPS 排名 |
| [进阶专题](docs/10-advanced.md) | 密码学、共识、EVM、DeFi 与合约安全 |
| [中文社区](docs/11-chinese-community.md) | 技术讨论、问答和开发者活动入口 |
| [Hyperledger Fabric](docs/12-hyperledger-fabric-path.md) | 联盟链架构、chaincode、组织治理与 Gateway 客户端 |
| [链上应用基础设施](docs/13-chain-app-infrastructure.md) | RPC、钱包 provider、交易状态与数据索引 |
| [Solidity 面试题](docs/solidity-interview.md) | 归档自测题，适合复习，不代替系统学习 |

## 安全事件复盘

| 日期 | 事件 | 攻击/风险主题 | 复盘 |
|---|---|---|---|
| 2026-09-24 | Bitget 热/温钱包被盗 | 第三方安全设备与钱包后台权限 | [阅读](events/2026/2026-09-24-bitget-hack.md) |
| 2025-10-11 | 加密市场大规模清算 | 杠杆、流动性与市场结构 | [阅读](events/2025/2025-10-11-crypto-crash.md) |
| 2025-02-21 | Bybit 冷钱包被盗 | Safe 前端供应链与签名流程 | [阅读](events/2025/2025-02-21-bybit-hack.md) |
| 2024-07-18 | WazirX 安全事件 | 多签流程与托管风险 | [阅读](events/2024/2024-07-18-wazirx-hack.md) |
| 2024-05-31 | DMM Bitcoin 被盗 | 交易所托管与资产缺口 | [阅读](events/2024/2024-05-31-dmm-bitcoin.md) |
| 2024-01 | Penpie 攻击 | DeFi 权限与市场操纵 | [阅读](events/2024/2024-01-penpie-hack.md) |
| 2022-11-11 | FTX 崩溃 | 托管、治理与客户资产隔离 | [阅读](events/2022/2022-11-11-ftx-collapse.md) |

事件日期、损失金额和归因都可能随调查更新。请以每篇文章的来源和资料边界为准；本文档只用于技术学习，不构成投资、交易或托管建议。

## 收录标准与维护

- 优先链接协议/工具官方文档、原始论文和可复现的实践材料；第三方内容注明作者、语言与用途。
- 新增资源要说明适合谁、解决什么问题，以及建议从哪一页或练习开始。
- 涉及版本、性能、监管、资金损失或攻击归因的内容必须附一手来源和核对日期；没有证据的说法标为推测或不收录。
- 失效、过时或有误的条目欢迎通过 Issue 或 Pull Request 提交修正。详见 [贡献指南](CONTRIBUTING.md)。

**最近整理：2026-10-12。** 外部链接和生态状态会变化，动态内容以链接目标的最新文档为准。

## License

文档内容采用 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)；所链接资源各自遵循其原有许可。
