# Bitcoin 开发学习路径

适合已有基础编程经验、希望理解 Bitcoin 协议或构建相关工具的读者。这里优先链接官方开发文档、协议资料和可实践资源。

## 建议顺序

1. **建立协议心智模型**：阅读[比特币白皮书](https://bitcoin.org/bitcoin.pdf)，重点理解点对点交易、工作量证明和交易链；白皮书不是完整的现代协议规格。
2. **理解数据结构与脚本**：跟随[Bitcoin Developer Guide](https://developer.bitcoin.org/devguide/)学习区块、交易、脚本、钱包、P2P 网络和挖矿。
3. **动手检查交易**：用 regtest 本地运行 Bitcoin Core，创建交易并检查输入、输出、脚本和区块；开发文档提供[示例与参考](https://developer.bitcoin.org/examples/)。
4. **跟进协议演进**：阅读 [BIP 仓库](https://github.com/bitcoin/bips)、[Bitcoin Optech](https://bitcoinops.org/) 和 Bitcoin Core 发布说明，区分提案、实现和已激活规则。
5. **再读实现代码**：从 [Bitcoin Core](https://github.com/bitcoin/bitcoin) 中与当前问题相关的模块开始，不建议初学者把通读整个仓库当作第一步。

## 推荐资料

- [Bitcoin Core 官方开发文档](https://bitcoincore.org/en/doc/) — RPC 与版本化参考资料。
- [Bitcoin Developer Documentation](https://developer.bitcoin.org/) — 协议指南、示例、参考和术语表。
- [Mastering Bitcoin（英文，在线阅读）](https://github.com/bitcoinbook/bitcoinbook) — Bitcoin 技术教材；以仓库当前版本和勘误为准。
- [Learn Me a Bitcoin](https://learnmeabitcoin.com/) — 通过图解解释区块、交易和脚本的第三方学习站点。
- [Bitcoin Optech](https://bitcoinops.org/) — 面向开发者与技术人员的协议和扩容技术通讯。
- [Bitcoin Stack Exchange](https://bitcoin.stackexchange.com/) — 技术问答；重要结论应回查规范、代码或官方文档。

## 学习时注意

- Bitcoin 白皮书年代较早，不能替代 BIP、当前实现和节点规则。
- Bitcoin Core 的 RPC、配置项和行为可能随版本变化，阅读文档时确认对应版本。
- 测试请使用 regtest 或 testnet 环境，不要把真实私钥、助记词或生产资金用于练习。
- “Bitcoin L2”涵盖不同信任与安全模型；评估具体系统时应读其协议和退出机制，不要仅凭标签判断。

*最后核对：2026-10-12。*
