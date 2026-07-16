---
layout: post
title: VSCode+HardHat搭建Solidity开发环境
date: 2025-08-03 13:23 +0800
---
# 使用VSCode + Hardhat部署智能合约并交互

在区块链开发中，部署和测试智能合约是核心环节。本文将详细介绍如何使用VSCode作为开发环境，结合Hardhat框架来部署一个简单的智能合约，并通过JavaScript脚本与合约进行交互。同时，我们也会解决国内用户常见的npm命令速度慢的问题。

## 一、准备工作

### 环境要求

- Node.js (v14.0.0及以上)
- npm 或 yarn
- VSCode
- Git

首先检查Node.js和npm是否已安装：

```bash
node -v
npm -v
```

如果未安装，请前往[Node.js官网](https://nodejs.org/)下载安装包进行安装。

### 解决npm速度慢的问题

国内用户经常遇到npm安装依赖速度慢的问题，主要原因是默认的npm仓库在国外。解决方法有两种：

1. **使用淘宝npm镜像**

```bash
# 临时使用
npm install --registry=https://registry.npmmirror.com

# 永久设置
npm config set registry https://registry.npmmirror.com

# 验证设置是否成功
npm config get registry
```

2. **使用nrm管理镜像源**

```bash
# 安装nrm
npm install -g nrm

# 查看可用镜像源
nrm ls

# 切换到淘宝镜像
nrm use taobao
```

推荐使用第二种方法，方便以后在不同镜像源之间切换。

## 安装VSCode及相关插件

1. 从[VSCode官网](https://code.visualstudio.com/)下载并安装VSCode
2. 安装以下推荐插件：
   - Solidity (by Juan Blanco) - Solidity语法高亮和提示
   - ESLint - 代码检查工具
   - Prettier - 代码格式化工具
   - Hardhat for VSCode - Hardhat集成

## 创建Hardhat项目

### 初始化项目

打开VSCode，创建一个新文件夹作为项目目录，然后打开终端（Ctrl+` 或 终端 > 新建终端）：

```bash
# 创建项目文件夹并进入
mkdir hardhat-demo && cd hardhat-demo

# 初始化npm项目
npm init -y

# 安装Hardhat
npm install --save-dev hardhat
```


### 创建Hardhat工程结构

```bash
# 运行Hardhat初始化命令
npx hardhat
```

运行后会出现交互式菜单，选择"Create an empty hardhat.config.js"，然后按回车确认。

### 安装必要依赖

```bash
# 安装以太坊相关库
npm install --save-dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai

# 安装dotenv用于管理环境变量
npm install dotenv --save
```

## 二、编写智能合约

在项目根目录创建`contracts`文件夹，然后在该文件夹下创建`Greeter.sol`文件：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Greeter {
    string private greeting;

    constructor(string memory _greeting) {
        greeting = _greeting;
    }

    function greet() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _greeting) public {
        greeting = _greeting;
    }
}
```

这是一个简单的合约，包含一个存储字符串的变量和两个函数：`greet()`用于获取字符串，`setGreeting()`用于设置字符串。

## 三、配置Hardhat

修改`hardhat.config.js`文件：

```javascript
require("@nomiclabs/hardhat-waffle");
require("dotenv").config();

// 从.env文件加载私钥
const PRIVATE_KEY = process.env.PRIVATE_KEY;

module.exports = {
  solidity: "0.8.4",
  networks: {
    // 配置本地网络
    hardhat: {},
    // 配置测试网（以Goerli为例）
    goerli: {
      url: `https://goerli.infura.io/v3/${process.env.INFURA_API_KEY}`,
      accounts: [`0x${PRIVATE_KEY}`]
    }
  }
};
```

在项目根目录创建`.env`文件，用于存储敏感信息：

```
# .env文件内容
PRIVATE_KEY=你的私钥（去掉0x前缀）
INFURA_API_KEY=你的Infura API密钥
```

> 注意：不要将`.env`文件提交到版本控制系统，在`.gitignore`中添加`.env`

## 四、创建部署脚本

在项目根目录创建`scripts`文件夹，然后创建`deploy.js`文件：

```javascript
const hre = require("hardhat");

async function main() {
  // 获取合约工厂
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  
  // 部署合约，构造函数参数为"Hello, Hardhat!"
  const greeter = await Greeter.deploy("Hello, Hardhat!");
  
  // 等待部署完成
  await greeter.deployed();

  console.log("Greeter deployed to:", greeter.address);
}

// 执行部署函数
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

## 五、创建交互脚本

在`scripts`文件夹下创建`interact.js`文件：

```javascript
const hre = require("hardhat");

async function main() {
  // 合约地址（部署后替换为实际地址）
  const contractAddress = "0x5FbDB2315678afecb367f032d93F642f64180aa3";
  
  // 连接到已部署的合约
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  const greeter = await Greeter.attach(contractAddress);
  
  // 调用greet()函数
  const currentGreeting = await greeter.greet();
  console.log("当前问候语:", currentGreeting);
  
  // 调用setGreeting()函数修改问候语
  console.log("设置新的问候语...");
  const tx = await greeter.setGreeting("Hello, Blockchain!");
  await tx.wait();
  
  // 再次调用greet()函数查看修改结果
  const newGreeting = await greeter.greet();
  console.log("新的问候语:", newGreeting);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

## 六、编译和部署合约

### 编译合约

```bash
npx hardhat compile
```

如果编译成功，会显示编译信息，并生成`artifacts`文件夹，包含合约的ABI等信息。

### 在本地测试网部署

```bash
npx hardhat run scripts/deploy.js --network hardhat
```

部署成功后，会输出合约地址，类似：`Greeter deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3`

### 与本地合约交互

将`interact.js`中的合约地址替换为部署时输出的地址，然后运行：

```bash
npx hardhat run scripts/interact.js --network hardhat
```

成功后会看到如下输出：

```
当前问候语: Hello, Hardhat!
设置新的问候语...
新的问候语: Hello, Blockchain!
```

### 在测试网部署（可选）

如果要部署到公共测试网（如Goerli），需要：

1. 注册[Infura](https://infura.io/)账号并创建项目，获取API密钥
2. 在MetaMask中获取测试网ETH（可以通过水龙头获取）
3. 运行部署命令：

```bash
npx hardhat run scripts/deploy.js --network goerli
```

部署成功后，可以在[Etherscan](https://goerli.etherscan.io/)上通过输出的合约地址查看合约信息。


## 七、Yarn 命令版本

可以选择使用yarn来替换npm

### 解决 Yarn 速度慢的问题
```bash
# 查看当前镜像源
yarn config get registry

# 永久切换到淘宝镜像
yarn config set registry https://registry.npmmirror.com

# 验证设置是否成功
yarn config get registry
```

### 使用 nrm 管理镜像源（Yarn 兼容）
```bash
# 全局安装 nrm（Yarn 方式）
yarn global add nrm

# 查看可用镜像源
nrm ls

# 切换到淘宝镜像
nrm use taobao
```

### 初始化Hardhat项目
```bash
# 创建项目文件夹并进入
mkdir hardhat-demo && cd hardhat-demo

# 初始化 Yarn 项目
yarn init -y

# 安装 Hardhat（开发依赖）
yarn add --dev hardhat
```

### 创建 Hardhat 工程结构
```bash
# 运行 Hardhat 初始化命令（与 npm 通用）
npx hardhat
```

### 安装必要依赖
```bash
# 安装以太坊相关库（开发依赖）
yarn add --dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai

# 安装 dotenv（生产依赖）
yarn add dotenv
```

### 编译合约
```bash
# 使用 Yarn 调用 Hardhat 编译
yarn hardhat compile
```

### 在本地测试网部署
```bash
yarn hardhat run scripts/deploy.js --network hardhat
```

### 与本地合约交互
```bash
yarn hardhat run scripts/interact.js --network hardhat
```

### 在测试网部署（可选）
```bash
yarn hardhat run scripts/deploy.js --network goerli
```


### 说明
- 所有 `npx hardhat` 命令均可替换为 `yarn hardhat`，功能完全一致
- Yarn 会生成 `yarn.lock` 文件替代 npm 的 `package-lock.json`，两者作用相同（锁定依赖版本）
- 其他操作（如编写合约、配置文件等）与 npm 版本完全一致，无需修改

使用时只需保持工具统一（全程用 Yarn 或全程用 npm），避免混用导致依赖冲突即可。