# 📘 区块链入门 101（零基础）

> 这一章写给**完全没接触过区块链的人**。建议顺序阅读。

---

## 第一部分：概念理解（先弄懂"是什么"）

### 1. 什么是区块链

**一句话**：去中心化的**分布式账本**，由网络中的多个节点共同维护。

**关键概念速览**：

| 概念 | 一句话 | 例子 |
|------|--------|------|
| **区块（Block）** | 一段时间内交易的"打包箱" | BTC ~10 分钟 / ETH ~12 秒 / Solana ~400ms |
| **链（Chain）** | 区块按顺序串起来的数据结构 | 每个区块包含上一个区块的哈希 → 形成"链" |
| **哈希（Hash）** | 一段数据加密后的"指纹" | SHA-256 / Keccak-256，相同输入永远相同输出 |
| **共识机制** | 多个节点如何"同意"下一个区块 | PoW（BTC）/ PoS（ETH）/ PoH（Solana）|
| **矿工 / 验证者** | 负责打包区块的节点 | BTC 矿工用算力，ETH 验证者质押 32 ETH |

### 2. 公链 vs 私链 vs 联盟链

| 类型 | 特点 | 代表 |
|------|------|------|
| **公链（Public）** | 完全开放，任何人可读写、验证 | BTC / ETH / Solana / Aptos / Sui |
| **联盟链（Consortium）** | 几个组织联合运营 | Hyperledger Fabric（Corda 等）|
| **私链（Private）** | 单一组织内部使用 | 企业内部账本 |

> 💡 我们这个仓库**主要讲公链**，因为公链生态最丰富、学习资源最多。

### 3. 钱包、私钥、地址、助记词

| 名词 | 比喻 | 关键 |
|------|------|------|
| **地址（Address）** | 银行卡号 | **可以公开**，用于收币 |
| **私钥（Private Key）** | 银行卡密码 + 身份证 | **绝对保密**，转出资产唯一凭证 |
| **助记词（Mnemonic）** | 私钥的备份形式 | 12/24 个英文单词，**丢了等于丢所有钱** |
| **钱包（Wallet）** | 管理私钥的工具 | 软钱包（App）/ 硬钱包（Ledger / Trezor）|

> 🚨 **核心安全规则**：
> - 助记词**抄在纸上**，绝不存手机/电脑/云端
> - 任何向你**要助记词**的人都是骗子（没有例外）
> - 硬件钱包（Ledger / Trezor）能挡 99% 的网络攻击

### 4. Gas / 交易 / 区块

| 概念 | 一句话 | 备注 |
|------|--------|------|
| **Gas** | 你为链上操作付的"燃料费" | ETH 主网 $1-$30 一笔交易；Solana < $0.01 |
| **交易（Tx）** | 你在链上做的任何操作 | 转账 / 调用合约 / 铸造 NFT |
| **区块（Block）** | 一批交易打包的结果 | ETH ~12 秒；BTC ~10 分钟；Solana ~400ms |

> 💡 **为什么需要 Gas？**：防止有人发垃圾交易攻击网络。手续费给打包交易的验证者作为奖励。

### 5. DeFi / NFT / DAO / 稳定币

| 概念 | 一句话 | 代表项目 |
|------|--------|----------|
| **DeFi** | 去中心化金融（不靠银行） | Uniswap / Aave / Compound / Curve |
| **NFT** | 链上唯一资产凭证 | OpenSea / Blur / Magic Eden |
| **DAO** | 去中心化自治组织 | MakerDAO / Uniswap DAO |
| **稳定币** | 锚定法币（$1）的代币 | USDT / USDC / DAI / USDe |

---

## 第二部分：术语速查表

> 第一次看到这些词会晕，先有个印象，遇到再回来看。

### 基础设施

| 术语 | 含义 |
|------|------|
| **节点（Node）** | 跑区块链软件的电脑 |
| **全节点 / 轻节点** | 全节点保存所有数据，轻节点只查自己需要 |
| **RPC** | 跟节点通信的接口（远程过程调用） |
| **区块浏览器** | 看链上数据的网站 | Etherscan / BscScan / Solscan |

### 交易相关

| 术语 | 含义 |
|------|------|
| **Nonce** | 同一地址的交易序号，防止重放 |
| **Mempool** | 待打包的交易池子（也叫 tx pool） |
| **Confirmations** | 交易被多少个后续区块"确认"了 |
| **Finality** | 交易"不可逆"的状态（ETH ~12 分钟，Solana 立即）|

### 代币相关

| 术语 | 含义 |
|------|------|
| **ERC-20** | ETH 上的同质化代币标准（如 USDT） |
| **ERC-721** | ETH 上的 NFT 标准 |
| **ERC-1155** | ETH 上的多代币标准（一笔交易发多种） |
| **SPL Token** | Solana 上的代币标准 |
| **Gas Token** | 用于支付 Gas 的币（ETH / SOL / BNB 等） |

### 高级概念

| 术语 | 含义 |
|------|------|
| **TVL（Total Value Locked）** | 协议里锁定的总资产价值（衡量 DeFi 协议规模） |
| **APY vs APR** | APY 含复利，APR 不含复利 |
| **流动性挖矿** | 把资产放进协议赚收益 |
| **无常损失** | 在 AMM 里做 LP 时，价格波动可能让你比单纯持有亏 |
| **预言机（Oracle）** | 把链下数据搬到链上的"信使"（如 Chainlink） |
| **跨链桥（Bridge）** | 把资产从一条链转到另一条链的工具 |

---

## 第三部分：实操入门（4 步走）

### Step 1：下载钱包（10 分钟）

推荐 **MetaMask**（ETH 系）或 **Phantom**（Solana 系）：

- MetaMask：[metamask.io](https://metamask.io/)
- Phantom：[phantom.app](https://phantom.app/)

**关键步骤**：
1. 安装浏览器扩展
2. 创建新钱包
3. **抄写助记词**（抄纸上！放保险箱！）
4. 验证助记词

### Step 2：领取测试币（30 分钟）

- ETH 测试币水龙头：[cloud.google.com/application/web3/faucet](https://cloud.google.com/application/web3/faucet)
- Sepolia / Holesky 测试网络 MetaMask 切换即可

### Step 3：发起第一笔交易（1 小时）

1. 切换到测试网
2. 领测试 ETH
3. 给自己另一个地址转 0.01 测试 ETH
4. 在 [sepolia.etherscan.io](https://sepolia.etherscan.io/) 查到这笔交易
5. 看到区块号 / confirmations / gas used

### Step 4：体验 DeFi / NFT（2 小时）

- 在 Uniswap 测试网 swap 一笔
- 在 OpenSea / Blur 铸造一个测试 NFT
- 在 Aave 测试网存入资产

---

## 第四部分：入门推荐资源（中文优先）

### 📖 科普文章（最友好的入门）

| 文章 | 链接 | 适合 |
|------|------|------|
| 简单易懂地介绍什么是区块链 | [知乎](https://zhuanlan.zhihu.com/p/22228902) | 完全零基础 |
| 简单易懂地介绍什么是区块链（技术篇）| [知乎](https://zhuanlan.zhihu.com/p/23243289) | 想懂技术原理 |
| 一文看懂区块链：一步一步发明比特币 | [CharlesLiu](https://charlesliuyx.github.io/2017/09/24/%E4%B8%80%E6%96%87%E7%9C%8B%E6%87%82%E5%8C%BA%E5%9D%97%E9%93%BE-%E4%BB%A5%E6%AF%94%E7%89%B9%E5%B8%81%E4%B8%BA%E4%BE%8B/) | 概念推导 |
| 区块链技术指南 | [yeasy](https://yeasy.gitbooks.io/blockchain_guide) | 系统化入门 |
| 共识算法与拜占庭将军问题 | [CharlesLiu](https://charlesliuyx.github.io/2018/03/03/) | 理解共识 |
| 一文看懂区块链架构设计 | [巴比特](http://www.8btc.com/ebook-blockchain) | 架构视角 |

### 🎬 可视化工具

- [Blockchain Demo](https://blockchaindemo.io/) — 可视化演示区块链原理
- [Bitcoin Demo](https://andersbrownworth.com/blockchain/) — BTC 区块演示

### 📜 白皮书（必读）

- 中本聪《Bitcoin: A Peer-to-Peer Electronic Cash System》[中文 PDF](https://bitcoin.org/files/bitcoin-paper/bitcoin_zh_cn.pdf)
- Vitalik《Ethereum White Paper》[中文](http://ethfans.org/wikis/%E4%BB%A5%E5%A4%AA%E5%9D%8A%E7%99%BD%E7%9A%AE%E4%B9%A6)

### 🎓 在线课程

| 课程 | 平台 | 备注 |
|------|------|------|
| Bitcoin and Cryptocurrency Technologies | Coursera | Princeton 课程（英文）|
| Defi Mooc 教程 | [defi-learning.org](https://defi-learning.org/) | DeFi 中文公开课 |

### 📚 学习路线图

- [Blockchain Roadmap](https://roadmap.sh/blockchain) — 按步骤规划
- [DeFi Developer Roadmap](https://github.com/OffcierCia/DeFi-Developer-Road-Map) — 开发者向

---

## 第五部分：常见误区

### ❌ 误区 1：区块链 = 比特币

> 区块链是底层技术，比特币是区块链的第一个应用。比特币只是区块链的一个 token。

### ❌ 误区 2：区块链 = 完全匿名

> 比特币、以太坊都是**伪匿名**。所有交易公开可查（Etherscan），FBI / Chainalysis 经常破案。真正匿名要用 Monero / Zcash 或混币器。

### ❌ 误区 3：私钥丢了能找回

> **完全不能**。私钥 / 助记词丢了 = 钱永久丢失。每年几百万美元 BTC 因为私钥丢失永久沉睡。

### ❌ 误区 4：放交易所 = 安全

> FTX 暴雷教过你：**Not your keys, not your coins**。交易所可能破产、被黑、跑路。大额资产一定自己保管。

### ❌ 误区 5：区块链 = Web3 = 元宇宙 = NFT = 暴富

> 这些是不同的东西，被营销绑在一起。区块链是技术，Web3 是应用层概念，元宇宙是另一种叙事。

---

## 🎯 给不同背景读者的建议

| 你是什么背景 | 推荐路径 |
|--------------|----------|
| **完全没听过区块链** | 1. 看 [知乎科普](https://zhuanlan.zhihu.com/p/22228902) → 2. 装 MetaMask → 3. 转一笔测试币 |
| **程序员但没接触过链** | 1. 装 MetaMask → 2. 看 [Solidity by Example](https://solidity-by-example.org/) → 3. 部署第一个合约 |
| **金融 / 投资背景** | 1. 读 BTC + ETH 白皮书 → 2. 看 DeFi 协议（Uniswap / Aave）→ 3. 了解 L2 与跨链 |
| **产品 / 运营** | 1. 了解 DeFi / NFT / DAO 是什么 → 2. 体验 Uniswap / OpenSea → 3. 看 [Web3 University](https://www.web3.university/) |

---

## 📚 下一步学习

完成本章后，建议顺序：

1. 📘 [入门 101](01-getting-started.md) ← 你在这里
2. 🛠️ [Solidity 学习路径](02-solidity-path.md) ← 程序员学这
3. ☀️ [Solana 学习路径](03-solana-path.md)
4. ₿ [Bitcoin 学习路径](04-bitcoin-path.md)
5. 🔬 [进阶专题](10-advanced.md) ← 深入理解

---

> ⚠️ **数据时效性**：本节基础概念稳定（BTC/ETH/NFT/DeFi 这些定义不会变），
> 但具体的项目 TVL / 排名变化快。本仓库**只做学习资源的整理**，不构成投资建议。

---

*最后更新: 2026-07-16*