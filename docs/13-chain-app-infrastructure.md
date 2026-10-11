# 链上应用基础设施：RPC、钱包与数据索引

这条路线补足“合约/程序写完后，应用怎样安全、稳定地读链和提交交易”。不同链使用不同账户、交易与确认模型；下面按概念对照，具体实现应回到对应链的 API 与规范。

## 应用数据与交易的路径

```text
用户操作 → 应用前端/后端 → 钱包签名（写操作） → RPC 节点/网关 → 区块链网络
                      ↘ 索引器/数据库 → 历史查询、搜索与应用视图
```

RPC 节点负责提供协议接口，不会自动提供所有产品所需的历史查询、业务聚合、用户活动列表或全文搜索。应用通常需要组合节点 API、钱包签名和索引/缓存层。

## 按生态学习 API

| 生态 | 读取/交易接口 | 客户端与关键点 |
|---|---|---|
| Ethereum / EVM | [Ethereum JSON-RPC](https://ethereum.org/developers/docs/apis/json-rpc/) · [Execution API 规范](https://github.com/ethereum/execution-apis) | 选择客户端库时核对网络、RPC 方法和 provider 行为；浏览器钱包 provider 参考 [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193)。 |
| Solana | [Solana RPC Reference](https://solana.com/docs/rpc) | 区分 HTTP 与 WebSocket、集群 endpoint 和 commitment；官方公共 RPC 是共享开发端点，不面向生产应用。 |
| Bitcoin | [Bitcoin Core RPC Reference](https://developer.bitcoin.org/reference/rpc/) | 从 regtest 和 Core RPC 入手；理解 UTXO、交易构造/签名及节点钱包 RPC 的边界。 |
| Hyperledger Fabric | [Fabric Gateway](https://hyperledger-fabric.readthedocs.io/en/latest/gateway.html) | 应用以组织身份连接 peer Gateway，处理评估、提交和交易状态；见 [Fabric 学习路径](12-hyperledger-fabric-path.md)。 |

## 钱包与签名

- 把**连接钱包、读取账户、切换网络、请求签名**视为不同操作；请求用户签名时说明将签什么、可能产生什么链上效果。
- 前端 provider 是钱包与应用之间的接口，并不意味着 RPC、钱包或应用彼此可信。校验当前网络、交易参数和返回状态。
- 不要在前端、服务器日志、Issue 或示例配置中保存私钥/助记词；服务端签名密钥应使用隔离的密钥管理方案。
- Ethereum 的 EIP-1193 描述 provider API，但它本身不规定钱包 UI、私钥安全或用户是否应相信某个 dApp。

## 索引与历史数据

- 小型应用可先直接调用 RPC，避免过早引入额外系统。
- 当需要按地址分页、跨合约关联、搜索或复杂历史视图时，评估自建索引器、托管索引服务或 [The Graph Subgraphs](https://thegraph.com/docs/en/subgraphs/overview/)；Subgraph 将链上事件/状态映射为可查询的数据模型。
- 索引结果是衍生数据。记录数据来源和索引高度，检查同步错误、重组处理、延迟与回填状态；关键写操作或资产判断应按业务要求向可信节点/合约状态复核。
- 区块浏览器适合人工检查交易和合约，不应默认当作应用的稳定后端 API。

## 动手练习：只读链上活动页

1. 选一个开发网络，使用 RPC 读取最新区块、指定交易回执和一份合约事件。
2. 保存网络标识、区块高度和交易哈希，展示失败状态与请求错误。
3. 订阅新块/日志后，主动断线重连，并去重处理同一日志；对可能重组的网络，明确展示确认状态。
4. 当数据需求超出 RPC 查询能力，再为指定合约事件建立索引，并与节点返回结果对照。
5. 只有在确有写操作需求时再接钱包：默认拒绝不清楚目标链、合约地址、调用数据或金额的签名请求。

## 上线前检查

- endpoint 的可用性、速率限制、归档/历史查询支持、WebSocket 断线恢复和故障切换；不要把公开测试端点当生产 SLA。
- 应用所连接的 chain/network 是否正确；不要只依赖用户可编辑的名称或前端显示文本。
- 交易回执、事件与索引高度是否有一致性策略；写入接口是否有幂等和重试处理。
- RPC key、服务端签名凭证和用户数据是否避免进入客户端 bundle、日志或公开仓库。
- 钱包连接/签名失败、用户拒绝、网络切换和交易未确认等路径是否都能清楚反馈。

*最后核对：2026-10-12。接口规范和服务能力会变化；以目标链、客户端与服务商当前文档为准。*
