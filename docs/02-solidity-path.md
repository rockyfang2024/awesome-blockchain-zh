# Solidity / EVM 学习路径

> 目标：写出一个小型 Solidity 合约，能在本地编译、测试、检查并解释它的安全边界。下面从官方文档和可复现练习开始。

## 开始前

- 会读写基本程序：变量、函数、条件、循环和命令行。
- JavaScript/TypeScript 不是学 Solidity 的前置条件；做 dApp 前端时再补即可。
- 学习与测试先用本地网络或测试环境，不要把真实资产或主网私钥放进练习项目。

## 建议顺序

| 步骤 | 资源 | 练习结果 |
|---|---|---|
| 1. 理解 Ethereum / EVM | [Ethereum 开发文档](https://ethereum.org/developers/docs/) · [技术介绍](https://ethereum.org/developers/docs/intro-to-ethereum/) | 能说明账户、交易、Gas、合约和 EVM 的关系 |
| 2. 学 Solidity 语法 | [Solidity 官方文档](https://docs.soliditylang.org/) · [Solidity by Example](https://solidity-by-example.org/) | 写一个有状态变量、事件、访问控制和错误处理的简单合约 |
| 3. 选开发环境 | [Foundry Book](https://book.getfoundry.sh/) 或 [Hardhat 文档](https://hardhat.org/docs) | 建立项目、编译合约，并能在本地网络部署 |
| 4. 使用成熟实现 | [OpenZeppelin Contracts 文档](https://docs.openzeppelin.com/contracts/) | 通过导入标准库实现 ERC-20 / ERC-721；避免重复造安全基础组件 |
| 5. 写测试并练安全 | [Ethereum 合约安全](https://ethereum.org/developers/docs/smart-contracts/security/) · [Ethernaut](https://ethernaut.openzeppelin.com/) | 为正常路径、失败路径和权限边界编写测试，并完成若干安全关卡 |

## 第一个项目建议

实现一个带有 owner 权限的简单投票或计数合约，至少包含：

1. 明确的状态变量和事件；
2. 对重复投票、无权限调用等失败条件的检查；
3. 对成功和失败路径的自动化测试；
4. 一份简短说明：谁能调用每个函数、哪些数据公开、哪些假设仍未验证。

完成后再进入代币、NFT、借贷等更复杂的主题。选协议源码阅读时，记录 commit 或发布版本，避免把旧教程与新工具的行为混为一谈。

## 安全练习

- [Ethernaut](https://ethernaut.openzeppelin.com/)：通过攻破故意设计有缺陷的合约练习常见漏洞。
- [Damn Vulnerable DeFi](https://www.damnvulnerabledefi.xyz/)：在隔离练习环境里分析 DeFi 攻击模式。
- [OpenZeppelin Contracts](https://github.com/OpenZeppelin/openzeppelin-contracts)：对照成熟库的实现和测试，而不是把示例代码直接当成生产方案。

## 参考入口

- [Solidity 官方文档](https://docs.soliditylang.org/) — 语言、编译器和安全说明；随版本变化。
- [Ethereum 开发者教程](https://ethereum.org/developers/tutorials/) — 按主题筛选的社区教程。
- [Foundry Book](https://book.getfoundry.sh/) — Forge、Cast、Anvil 等工具链。
- [Hardhat 文档](https://hardhat.org/docs) — JavaScript/TypeScript 开发环境。
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/) — 常用合约组件及 API 文档。

> **维护说明**：语言和工具文档是主入口；第三方课程属于补充材料。工具版本与教程发布日期请以原始文档为准。
