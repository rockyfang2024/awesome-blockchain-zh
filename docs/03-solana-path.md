# Solana / Rust 学习路径

> 目标：理解 Solana 的账户与交易模型，并用官方 Quickstart 或 Anchor 完成一个可测试的程序。工具安装和版本会变化，优先跟随 Solana / Anchor 官方文档。

## 建议顺序

| 步骤 | 资源 | 练习结果 |
|---|---|---|
| 1. 学 Rust 基础 | [The Rust Programming Language](https://doc.rust-lang.org/book/) · [Rust By Example](https://doc.rust-lang.org/rust-by-example/) | 理解所有权、借用、枚举、错误处理和 Cargo |
| 2. 理解 Solana 模型 | [Solana 官方文档](https://solana.com/docs) · [核心概念](https://solana.com/docs/core) | 解释账户、指令、交易、程序、PDA 和 CPI 的关系 |
| 3. 完成 Quickstart | [Build your first Solana program](https://solana.com/docs/intro/quick-start/build-first-program) | 编译、部署并调用第一个程序；先在本地或 devnet 操作 |
| 4. 选择框架 | [Anchor Quickstart](https://www.anchor-lang.com/docs/quickstart) · [原生 Rust 程序开发](https://solana.com/docs/programs/rust) | 用 Anchor 快速开发，或进一步理解不使用 Anchor 的底层接口 |
| 5. 做一个小项目 | [Solana Program Examples](https://solana.com/docs/programs/examples) | 从示例中选择 token、PDA 或转账练习，补上失败条件和测试 |

## 第一个项目建议

从计数器或简单留言板开始，检查并记录：

- 哪些账户由指令读取或修改，哪些账户必须签名；
- PDA 的种子和派生程序是否符合预期；
- 账户 owner、数据长度和权限约束是否在程序中验证；
- 成功路径、错误路径和重复调用是否都有测试。

Solana 文档目前建议初学者从 Anchor 入门；掌握账户模型后，再读原生 Rust 程序实现。不要把“能部署”当成安全审查的替代品。

## 工具与资料

- [Solana 开发者文档](https://solana.com/docs) — Quickstart、概念、程序、客户端和工具。
- [Solana 开发工具与示例](https://solana.com/docs/tools) — 本地开发、CLI、Bootcamp、Cookbook 和示例入口。
- [Anchor 文档](https://www.anchor-lang.com/docs) — 框架、CLI、测试与 API。
- [Rust 官方书](https://doc.rust-lang.org/book/) — Rust 基础；有其他语言版本时，以 Rust 官方站点为准。
- [Solana Stack Exchange](https://solana.stackexchange.com/) — 技术问答，提问时附最小复现和工具版本。

> **版本提示**：Solana/Agave CLI、Anchor 和 SDK 的版本演进较快。复制命令前先检查官方安装页和项目模板，不要混用旧教程中的版本号。
