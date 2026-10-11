# 🔥 热点事件分析

> 本仓库特色：每次区块链行业发生重大事件（被盗、暴雷、黑客攻击），做深度复盘，提取开发者/用户/协议设计者的学习点。

---

## 📋 全部事件（按时间倒序）

| 日期 | 事件 | 类型 | 核心 | 详细 |
|------|------|------|------|------|
| 2026-09-24 | Bitget 热/温钱包被盗 | 🔓 exchange_hack | 第三方安全设备入侵 + 伪造提现指令，约 $3.875 亿 | [→](2026/2026-09-24-bitget-hack.md) |
| 2025-02-21 | Bybit 冷钱包被盗 | 🔓 exchange_hack | Safe{Wallet} 前端攻击 | [→](2025/2025-02-21-bybit-hack.md) |
| 2024-07-18 | WazirX 暴雷 | 🔓 exchange_hack | Bybit 之前的同类预演 | [→](2024/2024-07-18-wazirx-hack.md) |
| 2024-05-31 | DMM Bitcoin 暴雷 | 💥 exchange_collapse | 日本持牌交易所倒闭 | [→](2024/2024-05-31-dmm-bitcoin.md) |
| 2024-01-xx | Penpie 协议攻击 | 🐛 defi_hack | 闪电贷 + 预言机操纵 | [→](2024/2024-01-penpie-hack.md) |
| 2022-11-11 | FTX 暴雷 | 💥 exchange_collapse | 挪用客户资金欺诈 | [→](2022/2022-11-11-ftx-collapse.md) |
| 2025-10-11 | 币圈史上最大爆仓 | 📉 market_event | 中美关税战 + DeFi 循环贷连环爆仓 | [→](2025/2025-10-11-crypto-crash.md) |

---

## 安全公司与取证团队报告精选

以下链接按**报告用途**整理，不是机构排名。安全审计/应急取证、智能合约根因分析和链上资金追踪解决的问题不同；链上资金流向分析不能单独证明入侵入口，阶段性取证也不应写成最终结论。金额、归因和统计口径请回到原文核对。

| 团队 | 代表性公开材料 | 主要用途与边界 |
|------|------|------|
| [慢雾 SlowMist](https://www.slowmist.com/report/) | [Bitget 事件阶段性调查报告（PDF，团队 GitHub）](https://github.com/slowmist/Knowledge-Base/blob/master/open-report-V2/incident-response/SlowMist%20Investigation%20Progress%20Report%20-%20Bitget_en-us.pdf)；[安全与反洗钱报告库](https://www.slowmist.com/report/) | 事件响应、威胁分析、链上追踪及年度/半年度态势；Bitget 报告是阶段性材料。 |
| [Mandiant / Google Cloud](https://cloud.google.com/security) | [Bitget Incident Response Status Report（2026-09-30，PDF）](https://img.bgstatic.com/multiLang/events/MFR26-1029_Status_Update_Bitget_0930.pdf) | 主机与企业网络取证；报告说明调查仍在进行，不应据此补写尚未公开的攻击者归因。 |
| [Beosin](https://beosin.com/resources/?type=7) | [Bitget 事件链上资金追踪](https://vaas.beosin.com/resources/a-comprehensive-on-chain-tracing-of-bitget-security-incident-)；[Bybit 事件追踪分析](https://vaas.beosin.com/resources/the-biggest-theft-of-144-bn-in-the-crypto-market---tracing-analysis-of-bybit-security-incident) | 资金路径、地址和跨链流向；追踪结果不等于主机入侵取证或根因结论。 |
| [CertiK](https://www.certik.com/) | [Bybit 事件技术分析](https://www.certik.com/blog/bybit-incident-technical-analysis)；[Hack3d 年度安全报告](https://www.certik.com/blog/hack3d-the-web3-security-report-2025) | 交易与合约分析、年度事故统计；统计需注意其事件定义和金额口径。 |
| [Chainalysis](https://www.chainalysis.com/) | [Bybit 事件与资金流分析](https://www.chainalysis.com/blog/bybit-exchange-hack-february-2025-crypto-security-dprk/)；[Bitget 被盗资金追踪](https://www.chainalysis.com/blog/387m-bitget-theft-2026/) | 链上归集、跨链流转与犯罪归因；归因是分析机构的判断，涉及官方归因时应同时链接执法机构公告。 |
| [TRM Labs](https://www.trmlabs.com/) | [Bybit 被盗资金追踪与归因](https://www.trmlabs.com/resources/blog/the-bybit-hack-following-north-koreas-largest-exploit) | 链上资金流和威胁组织分析；适合与其他分析团队、执法机构及交易所材料交叉核对。 |
| [PeckShield](https://peckshield.com/) | [PeckShield 官方研究与安全预警入口](https://peckshield.com/) | 以链上安全预警和研究为主；预警快讯适合发现事件，不能替代完整根因复盘。 |
| [BlockSec](https://blocksec.com/) | [Balancer V2 攻击根因分析](https://blocksec.com/blog/in-depth-analysis-the-balancer-v2-exploit)；[2025 重大安全事件索引](https://blocksec.com/blog/top-10-awesome-security-incidents-in-2025) | DeFi 合约漏洞和攻击交易分析；适合学习可复现的技术根因，不覆盖所有企业网络取证问题。 |
| [Verichains](https://github.com/verichains/public-audit-reports) | [Bybit 事件初步调查报告（PDF，GitHub）](https://github.com/verichains/public-audit-reports/blob/main/Bybit%20Incident%20Investigation%20-%20Preliminary%20Report%20v1.0%20%28for%20public%20release%29.pdf) | Bybit 委托的现场初步调查；阅读时注意报告标注的调查范围与初步结论。 |
| [Sygnia](https://www.sygnia.co/press-release/bybit-investigation-largest-crypto-heist-lazarus-group/) | [Bybit 调查结果发布](https://www.sygnia.co/press-release/bybit-investigation-largest-crypto-heist-lazarus-group/) | 事件响应与数字取证；该页面发布调查发现，详细判断应以其报告及适用范围为准。 |

**使用建议**：复盘单一事件时，先读受影响项目/服务方与受托取证团队的报告，再用至少一家独立安全研究团队核对技术路径，并用链上分析材料追踪资产流向。不同团队可能使用不同估值时间、损失定义和归因置信度；有冲突时保留各自口径，不强行合并成一个数字。

---

## 📊 按类型分组

### 🔓 exchange_hack（交易所攻击）

- [Bitget 热/温钱包被盗](2026/2026-09-24-bitget-hack.md) — 第三方安全设备漏洞导致内网凭证失窃，钱包后台提现校验被绕过
- [Bybit 冷钱包被盗](2025/2025-02-21-bybit-hack.md) — Safe{Wallet} 前端供应链攻击
- [WazirX 暴雷](2024/2024-07-18-wazirx-hack.md) — Bybit 之前的同类预演

### 💥 exchange_collapse（交易所倒闭）

- [DMM Bitcoin 暴雷](2024/2024-05-31-dmm-bitcoin.md) — 日本持牌交易所倒闭
- [FTX 暴雷](2022/2022-11-11-ftx-collapse.md) — 挪用客户资金欺诈

### 🐛 defi_hack（DeFi 协议攻击）

- [Penpie 协议攻击](2024/2024-01-penpie-hack.md) — 闪电贷 + 预言机操纵

### 📉 market_event（市场行情事件）

> **2025 新增类型**：除了安全事件，现在也记录**市场行情剧烈波动**事件。
> 这类事件的特征：
> - 不是被黑、不是欺诈，而是市场/技术/政策驱动的崩盘
> - 通常伴随大额爆仓 + 连锁反应
> - 教训主要给交易者、交易所运营者、监管观察者

- [2025-10-11 币圈史上最大爆仓（192 亿美元）](2025/2025-10-11-crypto-crash.md) — 中美关税战 + DeFi 循环贷连环爆仓，wbETH 跌至 0.2 ETH

**典型案例**（未来可补充）：
- 2021-05-19 中国监管 + Elon Musk 推文 → BTC 从 4.3 万跌到 3 万
- 2022-05 UST/LUNA 崩盘 → LUNA 从 80 美元跌到接近 0
- 2022-11 FTX 暴雷 → BTC 从 2 万跌到 1.5 万
- 2024-08 鲍威尔讲话 + 日本加息 → 全球流动性危机，BTC 从 6.5 万跌到 4.9 万

---

## 🎓 通用教训（跨所有事件）

| 教训 | 适用对象 |
|------|----------|
| **not your keys, not your coins** | 所有持币者 |
| **多签 + 硬件钱包屏幕核对** | 资金管理者 |
| **POR 不是 100% 证明** | CEX 用户 |
| **预言机用单源 = 自杀** | DeFi 开发者 |
| **前端是攻击面** | Web3 工程师 |
| **大额资产分散持有** | 所有持币者 |
| **交易所技术故障 = 黑天鹅** | 交易者（行情类事件）|
| **杠杆是双刃剑** | 交易者（行情类事件）|
| **监管黑天鹅无法预测** | 投资者（行情类事件）|

---

## ✍️ 贡献新事件

请按以下模板在 `events/YYYY/` 下创建 markdown：

```markdown
# 事件名（YYYY-MM）

> **事件类型**: exchange_hack / exchange_collapse / defi_hack / market_event / other
> **金额**: 约 X 亿美元（如果是行情类事件，可标价格变化）
> **核心问题**: 一句话总结

## 时间线
## 攻击原理 / 问题根源 / 触发原因
## 学习要点（分开发者/用户/协议设计者/交易者）
## 参考资料
```

⚠️ **数据时效性**：事件细节（金额、攻击者、追回情况）可能快速变化。
所有数据基于公开报道 + 链上分析，**不代表官方最终结论**。
本仓库**不提供投资建议**，只做学习资源的整理和事件的分析框架。
