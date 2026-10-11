# 📚 区块链书籍与白皮书

本页把**面向读者的书籍**和**协议原始论文/白皮书**分开整理。白皮书适合理解设计背景，不等同于持续更新的协议规范；学习实现细节时，请优先看各项目当前官方文档。

## 中文科普与入门

| 书名 | 作者 / 出版信息 | 适合读者 | 正版或权威入口 |
|------|------|------|------|
| [《小岛区块链：比特币、区块链、数字资产和通证的故事》](https://read.douban.com/ebook/150902091/) | 方军；中信出版社，2020；ISBN 9787521717549 | 通过故事和插图了解比特币、区块链应用与通证概念 | [中信出版社提供的豆瓣阅读电子书](https://read.douban.com/ebook/150902091/) |
| 《区块链：从数字货币到信用社会》 | 长铗 / 韩锋 | 了解区块链早期概念与应用讨论 | [出版社/书目检索](https://search.jd.com/Search?keyword=%E5%8C%BA%E5%9D%97%E9%93%BE%20%E4%BB%8E%E6%95%B0%E5%AD%97%E8%B4%A7%E5%B8%81%E5%88%B0%E4%BF%A1%E7%94%A8%E7%A4%BE%E4%BC%9A) |
| 《比特币：一个虚幻而真实的金融未来》 | 李钧 / 长铗 | 了解比特币早期发展脉络；出版时间较早，建议结合当前资料阅读 | [书目检索](https://search.jd.com/Search?keyword=%E6%AF%94%E7%89%B9%E5%B8%81%20%E4%B8%80%E4%B8%AA%E8%99%9A%E5%B9%BB%E8%80%8C%E7%9C%9F%E5%AE%9E%E7%9A%84%E9%87%91%E8%9E%8D%E6%9C%AA%E6%9D%A5) |
| 《以太坊技术详解与实战》 | 汪晓明 | 了解以太坊与智能合约基础；实践内容需对照当前 Solidity / Ethereum 文档更新 | [书目检索](https://search.jd.com/Search?keyword=%E4%BB%A5%E5%A4%AA%E5%9D%8A%E6%8A%80%E6%9C%AF%E8%AF%A6%E8%A7%A3%E4%B8%8E%E5%AE%9E%E6%88%98) |

《小岛区块链》是科普读物，不是协议实现手册，且书中涉及的行业背景会随时间变化。当前可核实的正版入口由中信出版社提供；**暂未找到作者或出版社授权、可在 GitHub 免费分发的 PDF**，因此不收录来源不明的扫描件或网盘镜像。购买/阅读入口见上表。

## 开放获取的技术书籍

下列链接是作者/项目维护的 GitHub 全文或源稿仓库。仓库提供可在线阅读的内容，但不一定附有可直接下载的 PDF；请以仓库许可证和 README 的说明为准。

| 书名 | 内容 | GitHub 正版源 |
|------|------|------|
| [Mastering Bitcoin](https://github.com/bitcoinbook/bitcoinbook) | 比特币协议、交易、钱包与节点；适合有一定技术基础的读者 | [bitcoinbook/bitcoinbook](https://github.com/bitcoinbook/bitcoinbook)（各版许可不同；第三版为 CC BY-SA 4.0） |
| [Mastering Ethereum, 2nd Edition](https://github.com/ethereumbook/ethereumbook) | 以太坊与智能合约开发原理 | [ethereumbook/ethereumbook](https://github.com/ethereumbook/ethereumbook)（仓库说明采用 Creative Commons 许可；查看仓库当前许可条款） |

## 主流公链白皮书与官方资料

| 项目 | 白皮书 / 代表性论文 | 官方网站与当前文档 | 阅读提示 |
|------|------|------|------|
| Bitcoin | [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf) · [中文及其他版本](https://bitcoin.org/en/bitcoin-paper) | [Bitcoin.org](https://bitcoin.org/) · [Bitcoin Developer Guide](https://developer.bitcoin.org/) | 2008 年原始设计论文；开发参考还应看当前开发者文档与 Bitcoin Core。 |
| Ethereum | [Ethereum Whitepaper](https://ethereum.org/whitepaper/) | [Ethereum.org](https://ethereum.org/) · [开发者文档](https://ethereum.org/developers/docs/) | 2014 年白皮书用于了解愿景；官网明确提示它已不能完整代表今天的以太坊。 |
| Solana | [Solana 白皮书 PDF](https://solana.com/solana-whitepaper.pdf) | [Solana](https://solana.com/) · [官方文档](https://solana.com/docs) | 重点是 Proof of History 的早期设计论述；当前架构和开发以现行文档为准。 |
| Polkadot | [Polkadot Whitepaper](https://polkadot.com/papers/Polkadot-whitepaper.pdf) | [Polkadot](https://polkadot.com/) · [开发者文档](https://docs.polkadot.com/) | 原始愿景论文形成于早期设计阶段；需结合当前协议规范和文档理解已演进的架构。 |
| Cosmos | [Cosmos Whitepaper（原始愿景）](https://legacy.cosmos.network/whitepaper/) | [Cosmos](https://cosmos.network/) · [开发者文档](https://docs.cosmos.network/) | 官方将原始白皮书归为历史愿景材料；当前模块化技术栈应分别阅读 Cosmos SDK、CometBFT 与 IBC 文档。 |
| Cardano | [Cardano Research](https://cardano.org/research/)（Ouroboros 等论文） | [Cardano](https://cardano.org/) · [开发者文档](https://developers.cardano.org/docs/) | Cardano 的共识设计主要由同行评审论文和协议规范介绍，并无一个能概括当前全链的单一白皮书。 |
| Avalanche | [Avalanche 共识论文](https://assets-global.website-files.com/5d80307810123f5ffbb34d6e/6009805681b416f34dcae012_Avalanche%20Consensus%20Whitepaper.pdf) | [Avalanche](https://avax.network/) · [官方文档](https://build.avax.network/docs) | 这是 Avalanche 共识的代表性论文，不是涵盖所有 Avalanche 功能的完整现行规格。 |
| Aptos | [Aptos White Paper](https://aptos.dev/network/blockchain/aptos-white-paper) · [PDF](https://aptosnetwork.com/whitepaper/aptos-whitepaper_en.pdf) | [Aptos](https://aptos.dev/) | 白皮书介绍 Aptos 的设计与 Move；实施细节以现行文档为准。 |
| Sui | [Sui 技术白皮书 PDF](https://docs.sui.io/paper/sui.pdf) · [研究论文索引](https://docs.sui.io/references/research-papers) | [Sui](https://www.sui.io/) · [官方文档](https://docs.sui.io/) | 白皮书用于了解对象模型和共识设计；研究论文与官方文档会覆盖更多后续演进。 |
| TON | [TON Whitepaper PDF](https://ton.org/en/whitepaper.pdf) | [TON](https://ton.org/) · [官方文档](https://docs.ton.org/) | 原始白皮书是早期设计材料；官方文档将白皮书中的概念整理到当前技术说明中。 |
| TRON | [TRON 白皮书 v2.1 PDF](https://tron.network/static/doc/white_paper_v_2_1.pdf) | [TRON](https://tron.network/) · [开发者文档](https://developers.tron.network/docs) | 请注意白皮书版本；接口、虚拟机和节点行为以当前开发者文档为准。 |
| BNB Smart Chain | —（本页未找到可作为当前完整规范的单一白皮书） | [BNB Chain](https://www.bnbchain.org/) · [BSC 官方文档](https://docs.bnbchain.org/bnb-smart-chain/) | 阅读当前共识、最终性与升级机制时，以官方文档及对应 BEP 提案为准。 |
| Polygon PoS | —（优先使用当前技术文档和规范） | [Polygon](https://polygon.technology/) · [Polygon 技术文档](https://docs.polygon.technology/) | Polygon 品牌涵盖多个网络与技术方案；阅读时先确认材料对应的是 Polygon PoS、zkEVM 还是其他组件。 |

### 延伸：许可链

| 项目 | 代表性技术资料 | 官方文档 |
|------|------|------|
| Hyperledger Fabric | [Hyperledger Fabric: A Distributed Operating System for Permissioned Blockchains](https://arxiv.org/abs/1801.10228)（学术论文，并非公链白皮书） | [Fabric 官方文档](https://hyperledger-fabric.readthedocs.io/) |

## 建议阅读顺序

1. 先读一本科普书，建立交易、区块、共识和智能合约的基本概念。
2. 再读 Bitcoin 或 Ethereum 的原始论文，理解它们试图解决的问题及早期设计取舍。
3. 想学习具体开发时，转到链的官方文档、协议规范、改进提案和代码仓库；不要只按旧白皮书推断当前主网行为。
4. 阅读安全、共识和经济机制时，优先使用项目研究页列出的论文，并核对论文版本、发布日期和适用网络。

> 本页收录的是学习入口，不代表对相关网络、书籍或资产的投资建议。链接和版本可能变化，欢迎通过 PR 提交官方来源或勘误。
