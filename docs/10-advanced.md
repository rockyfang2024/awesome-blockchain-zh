# 🔬 进阶专题

## 密码学基础

- 哈希函数（SHA-256 / Keccak-256）
- 椭圆曲线签名（ECDSA / Ed25519）
- 零知识证明（ZK-SNARK / ZK-STARK）
- BLS 签名聚合

## 共识机制

- PoW（工作量证明）— BTC 早期、ETH 早期
- PoS（权益证明）— ETH 现行
- PoH（历史证明）— Solana
- Tendermint BFT — Cosmos
- HotStuff — Facebook Libra / Aptos

## DeFi 协议剖析

- AMM（Uniswap V2/V3/V4）
- 借贷（Aave / Compound）
- 稳定币（[机制与实现专题](15-stablecoins.md)，以 Sky / DAI、USDC、USDT 为例）
- 衍生品（dYdX / GMX）
- 收益聚合器（Yearn）

## 安全

- 常见漏洞：重入、抢跑、闪电贷攻击
- 审计工具：Slither / Mythril / Echidna
- 审计公司：OpenZeppelin / Trail of Bits / SlowMist

## 大学公开课

| 课程 | 学校 | 链接 |
|------|------|------|
| Bitcoin and Cryptocurrency Technologies | Princeton | Coursera |
| Blockchain at Berkeley | UC Berkeley | YouTube |
| Bitcoin and Cryptocurrency Technologies | Princeton | [Coursera 课程](https://www.coursera.org/learn/cryptocurrency)；课程开放情况以平台页面为准 |

## 延伸学习顺序

建议先选定一个生态，再围绕一个问题读文档、源码和测试。不要把协议名称或安全工具清单当成已经掌握该主题；每个练习应记录所用版本、运行环境和未覆盖的假设。

- EVM 合约与测试：见 [Solidity / EVM 学习路径](02-solidity-path.md)。
- Solana 程序与账户约束：见 [Solana / Rust 学习路径](03-solana-path.md)。
- 事件攻击链与防护边界：见 [安全事件复盘索引](../events/README.md)。

*最后核对：2026-10-12。*
