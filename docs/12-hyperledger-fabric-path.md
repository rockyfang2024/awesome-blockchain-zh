# Hyperledger Fabric 联盟链开发路径

本方向补足公链开发之外的许可型分布式账本。Fabric 的组织身份、策略治理和数据隔离模型与公链不同；适合需要多组织协作、权限控制和可审计流程的开发/架构学习，不代表采用区块链本身就能解决组织治理或数据可信问题。

## 建议顺序

| 阶段 | 官方资料 | 目标 |
|---|---|---|
| 1. 了解架构 | [Fabric 文档总览](https://hyperledger-fabric.readthedocs.io/en/latest/) · [关键概念](https://hyperledger-fabric.readthedocs.io/en/latest/whatis.html) | 说清 Peer、Orderer、组织、Channel、账本与应用之间的关系 |
| 2. 本地启动 | [Getting Started](https://hyperledger-fabric.readthedocs.io/en/latest/getting_started.html) · [Test Network 教程](https://hyperledger-fabric.readthedocs.io/en/latest/test_network.html) | 用本地测试网络建通道、部署示例 chaincode 并理解各容器角色 |
| 3. 编写业务逻辑 | [Writing Your First Chaincode](https://hyperledger-fabric.readthedocs.io/en/latest/chaincode4ade.html) · [Smart Contracts and Chaincode](https://hyperledger-fabric.readthedocs.io/en/latest/smartcontract/smartcontract.html) | 用 Go、Java 或 JavaScript/TypeScript 示例实现资产读写和访问约束 |
| 4. 理解部署治理 | [Chaincode Lifecycle](https://hyperledger-fabric.readthedocs.io/en/latest/chaincode_lifecycle.html) · [Endorsement Policies](https://hyperledger-fabric.readthedocs.io/en/latest/endorsement-policies.html) | 追踪组织安装、批准、提交定义与背书策略的关系 |
| 5. 构建客户端 | [Fabric Gateway](https://hyperledger-fabric.readthedocs.io/en/latest/gateway.html) · [Running a Fabric Application](https://hyperledger-fabric.readthedocs.io/en/latest/write_first_app.html) | 从 Go、Node.js 或 Java 应用连接 Gateway，提交交易并处理提交状态 |
| 6. 学身份与数据边界 | [MSP 身份模型](https://hyperledger-fabric.readthedocs.io/en/latest/membership/membership.html) · [Private Data](https://hyperledger-fabric.readthedocs.io/en/latest/private-data/private-data.html) | 区分组织成员身份、通道可见性、私有数据集合和背书规则 |
| 7. 了解运维差异 | [生产网络部署](https://hyperledger-fabric.readthedocs.io/en/latest/deployment_guide_overview.html) · [What's New / Release Notes](https://hyperledger-fabric.readthedocs.io/en/latest/whatsnew.html) | 关注证书轮换、备份恢复、监控、升级与版本支持策略 |

## 动手项目

用 `fabric-samples` 的 `asset-transfer-basic` 做一个资产登记/流转小应用：

1. 在本地 Test Network 启动两家组织和一个 channel。
2. 部署示例 chaincode；观察各组织如何批准并提交相同的 chaincode definition。
3. 用 Gateway 客户端创建资产、查询状态、提交更新，并处理交易已提交/失败的结果。
4. 增加一个角色或组织检查，再加入覆盖无权限、重复写入和并发更新的测试。
5. 记录每条数据由哪些组织可见、哪些组织必须背书，以及这些策略变更需要什么治理流程。

## 关键概念与常见误解

- **Chaincode 与 smart contract**：业务合约由 Fabric 的生命周期安装并部署到 channel；部署本身要求通道成员按策略达成一致。
- **背书不是“任意节点签名”**：背书策略定义交易验证需要哪些组织的 peer 执行并背书，策略设计是业务治理的一部分。
- **Channel 不等于所有隐私需求**：通道隔离账本成员；需在同一通道内对部分组织隐藏数据时，研究 Private Data Collections 及其分发、背书和清理限制。
- **Gateway 简化客户端，不取消信任边界**：Fabric Gateway 在 peer 侧协调提案评估、背书和提交；应用仍需正确配置身份、目标组织、超时和提交状态处理。
- **测试网络不是生产蓝图**：官方文档明确 Test Network 仅供学习和测试。生产部署需依据独立的生产网络指南设计多组织运维、密钥/证书管理、容灾和升级治理。

## 版本与维护

Fabric 文档维护有版本支持与升级说明。开始项目前先确认目标版本、语言客户端和部署工具相互兼容；教程中的命令和示例应以对应版本文档为准。文档当前将 Fabric v2.5 列为 LTS 版本，同时维护后续版本说明；具体支持状态以官方发布页为准。

*最后核对：2026-10-12。*
