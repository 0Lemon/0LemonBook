# 部署智能合约

## 以太坊智能合约课

### 第03课--部署智能合约

#### 1.部署到Truffle

**Truffle中文文档地址：**

> [https://learnblockchain.cn/docs/truffle/index.html](https://learnblockchain.cn/docs/truffle/index.html)

**1.安装 Truffle：**

```text
npm install -g truffle
```

**2.新建项目文件夹**

```text
mkdir myProject    
cd myProject
truffle init
```

**3.安装Openzeppelin**

```text
npm install @openzeppelin/contracts
```

**4.创建Token.sol**

```text
vim contracts/Token.sol
```

```text
pragma solidity ^0.5.0;
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/ERC20Detailed.sol";
contract ExampleToken is ERC20, ERC20Detailed {
  constructor () public
  ERC20Detailed("CuiToken", "CUI", 18){
    _mint(msg.sender,10000000000 * (10 ** uint256(decimals())));
  }
}
```

**5.编译**

```text
truffle compile
```

**6.创建文件**

```text
vim migrations/2_deploy_contracts.js
```

```text
const ExampleToken = artifacts.require("ExampleToken");

module.exports = function(deployer) {
  deployer.deploy(ExampleToken);
};
```

**7.部署到Truffle develop**

```text
truffle develop
```

```text
migrate
```

**8.合约调用**

```text
var myCoin
ExampleToken.deployed().then(function(instance){myCoin=instance})
```

#### 2.部署到Ganache

**1.修改truffle-config.js文件**

```text
vim truffle-config.js
```

```text
module.exports = {
  	networks: {
      development: {
        host: "192.168.1.30",     // Localhost (default: none)
        port: 7545,            // Standard Ethereum port (default: none)
        network_id: "*",       // Any network (default: none)
      },
    }
};
```

**2.部署到Ganache**

```text
truffle console
```

```text
migrate
```

**3.合约调用**

```text
var myCoin
ExampleToken.deployed().then(function(instance){myCoin=instance})
```

#### 3.部署到Ropsten

**1.安装HDWalletProvider**

```text
npm install @truffle/hdwallet-provider
```

**2.获取Ropsten测试币**

**获取地址：**

> [https://faucet.ropsten.be/](https://faucet.ropsten.be/)

![](../../.gitbook/assets/image%20%284%29.png)

**3.获取MetaMask助记词**

![](../../.gitbook/assets/image%20%2853%29.png)

**4.注册Infura，获取测试网或主网的KEY**

**地址：**

> [https://infura.io/](https://infura.io/)

![](../../.gitbook/assets/image%20%2880%29.png)

**5.修改truffle-config.js文件**

```text
vim truffle-config.js
```

```text
var HDWalletProvider = require("truffle-hdwallet-provider");  // 导入模块
var mnemonic = "oppose say prevent raven mystery fiber program pupil poverty else pill enact";  //MetaMask的助记词。

module.exports = {
  	networks: {
        ropsten: {
            provider: function() {
                // mnemonic表示MetaMask的助记词。 "ropsten.infura.io/v3/33..."表示Infura上的项目id
                return new HDWalletProvider(mnemonic, "https://ropsten.infura.io/v3/e1bb25c2b20b4b5383517028056c89a3", 1);   // 0表示第二个账户(从0开始)
            },
            network_id: "*",  // match any network
            gas: 3012388,
            gasPrice: 20000000000,
            confirmations: 2,    // # of confs to wait between deployments. (default: 0)
            timeoutBlocks: 200,  // # of blocks before a deployment times out  (minimum/default: 50)
            skipDryRun: true     // Skip dry run before migrations? (default: false for public nets )
        },
  	}
};
```

**6.部署**

```text
truffle migrate  --network ropsten
```

**7.合约调用**

```text
truffle console --network ropsten
```

```text
var myCoin
ExampleToken.deployed().then(function(instance){myCoin=instance})
```

#### 4.部署到主网

**1.修改truffle-config.js文件**

```text
vim truffle-config.js
```

```text
var HDWalletProvider = require("@truffle/hdwallet-provider");  // 导入模块
var mnemonic_mainnet = "主网助记词";  //MetaMask的助记词。

module.exports = {
  	networks: {
      mainnet: {
        provider: new HDWalletProvider(mnemonic_mainnet, "https://mainnet.infura.io/e1bb25c2b20b4b5383517028056c89a3"),
        network_id: 1,
        gas: 3012388,
        gasPrice: 20000000000,
        confirmations: 2,    // # of confs to wait between deployments. (default: 0)
        timeoutBlocks: 200,  // # of blocks before a deployment times out  (minimum/default: 50)
        skipDryRun: true     // Skip dry run before migrations? (default: false for public nets )
      }
  	}
};
```

**2.部署**

```text
truffle migrate  --network mainnet
```

**3.合约调用**

```text
truffle console --network mainnet
```

```go
var myCoin
ExampleToken.deployed().then(function(instance){myCoin=instance})
```

## 学习结束了，给作者来杯咖啡？

{% page-ref page="../../0lemon/coffee.md" %}

