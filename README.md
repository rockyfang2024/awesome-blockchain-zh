# awesome-blockchain-zh

> 🎯 GitHub 上学习区块链最全的中文资源仓库。覆盖 Ethereum / Solana / BTC 等主流 L1/L2，从入门到精通。

---

## 🚀 快速导航

| 我是... | 推荐入口 |
|---------|----------|
| 完全新手 | [📘 入门 101](docs/01-getting-started.md) |
| 想学 Solidity | [🛠️ Solidity 学习路径](docs/02-solidity-path.md) |
| 学 Solana / Rust | [☀️ Solana 学习路径](docs/03-solana-path.md) |
| 学 BTC 底层 | [₿ Bitcoin 学习路径](docs/04-bitcoin-path.md) |
| 找视频课 | [🎬 视频教程](docs/05-videos.md) |
| 找书 | [📚 必读书单](docs/06-books.md) |
| 想做项目 | [💻 推荐开源项目](docs/07-projects.md) |
| 想跟前沿 | [📰 信息源](docs/08-info-sources.md) |
| 准备面试 | [🎯 Solidity 面试题](docs/solidity-interview.md) |
| 找交易所 | [🏦 交易所列表](docs/12-exchanges-referrals.md) |
| 币圈内推 | [💼 内推资源](docs/12-exchanges-referrals.md) |
| 看行业事件 | [🔥 热点事件分析](events/) |

---

## 📚 资源模块

按主题拆分，详情见 `docs/` 子目录：

| 模块 | 内容 |
|------|------|
| [📘 入门 101](docs/01-getting-started.md) | 区块链是什么、公链类型、钱包、Gas、DeFi/NFT/DAO |
| [🛠️ Solidity](docs/02-solidity-path.md) | 学习路径 + 推荐资源 + 知识笔记 |
| [☀️ Solana](docs/03-solana-path.md) | Rust 基础 + Anchor 框架 + 推荐教程 |
| [₿ Bitcoin](docs/04-bitcoin-path.md) | 白皮书 + Mastering Bitcoin + 源码 |
| [🌐 L1 / L2 生态](docs/09-l1-l2.md) | 9 条 L1 对比 + 5 种 L2 类型 |
| [🔬 进阶专题](docs/10-advanced.md) | 密码学、共识机制、DeFi 协议、安全审计 |
| [🎬 视频教程](docs/05-videos.md) | B 站 + YouTube + 在线交互 |
| [📚 必读书单](docs/06-books.md) | 中文 + 英文 + 论文 |
| [💻 推荐开源项目](docs/07-projects.md) | 按语言分类（Go / Rust / Solidity） |
| [📰 信息源](docs/08-info-sources.md) | 公众号 / Newsletter / Twitter / 数据平台 |
| [🇨🇳 中文社区](docs/11-chinese-community.md) | 论坛 / Discord / 媒体 / 会议 |
| [🏦 交易所 + 内推](docs/12-exchanges-referrals.md) | CEX/DEX 列表 + 币圈公司内推 |

---

## 🔥 热点事件分析

> 本仓库特色：每次区块链行业发生重大事件（被盗、暴雷、黑客攻击、行情剧烈波动），做深度复盘，提取开发者/用户/协议设计者/交易者的学习点。

| 日期 | 事件 | 类型 | 核心 | 详细 |
|------|------|------|------|------|
| 2025-02-21 | Bybit 冷钱包被盗 | 🔓 exchange_hack | Safe{Wallet} 前端攻击，~$15 亿 | [→](events/2025/2025-02-21-bybit-hack.md) |
| 2024-07-18 | WazirX 暴雷 | 🔓 exchange_hack | Bybit 之前的同类预演，$2.34 亿 | [→](events/2024/2024-07-18-wazirx-hack.md) |
| 2024-05-31 | DMM Bitcoin 暴雷 | 💥 exchange_collapse | 日本持牌交易所倒闭，$3.08 亿 | [→](events/2024/2024-05-31-dmm-bitcoin.md) |
| 2024-01-xx | Penpie 协议攻击 | 🐛 defi_hack | 闪电贷 + 预言机操纵，~$2700 万 | [→](events/2024/2024-01-penpie-hack.md) |
| 2022-11-11 | FTX 暴雷 | 💥 exchange_collapse | 挪用客户资金欺诈，$80 亿缺口 | [→](events/2022/2022-11-11-ftx-collapse.md) |
| 2025-10-11 | 币圈史上最大爆仓（192 亿美元） | 📉 market_event | 中美关税战 + DeFi 循环贷连环爆仓 | [→](events/2025/2025-10-11-crypto-crash.md) |

### 通用教训

- **not your keys, not your coins** — 大额资产自己保管
- **多签 + 硬件钱包屏幕核对** — 多签不是银弹，前端 UI 也可能被攻击
- **POR 不是 100% 证明** — FTX 当时也有 POR
- **预言机用单源 = 自杀** — DeFi 协议预言机要冗余
- **前端是攻击面** — Bybit / WazirX 都因前端 UI 被入侵
- **大额资产分散持有** — 别 all-in 一家交易所

详情模板见 [events/ 目录](events/)。

---

## ⚠️ 数据时效性

本仓库所有数据（事件、链接、价格、TVL）都可能快速变化。任何具体数字请以原始来源为准。
本仓库**只做学习资源的整理和事件的分析框架**，不提供投资建议。

---

## 🚧 贡献

欢迎提交 PR 补充资源或修正错误：
- 资源真实可用（链接能打开）
- 中文资源优先
- 简短说明为什么推荐（一句话）
- 按类别放到对应模块

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

---

⭐ 如果这个仓库对你有帮助，请 Star 支持！
