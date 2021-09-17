# Hello Word

## 以太坊智能合约课

### 第01课

#### Remix工具地址：

[https://remix.ethereum.org/](https://remix.ethereum.org/)

#### MetaMask安装地址：

[https://metamask.io/](https://metamask.io/)

#### 以太坊浏览器地址：

[https://blockexplorer.one/eth/ropsten](https://blockexplorer.one/eth/ropsten)

#### 合约代码：

```go
pragma solidity >=0.4.22 <0.6.0;
contract HelloWorld{
    string _name;
    function setName(string name) public{
        _name = name;
    }
    function getName() constant public returns(string){
        return _name;
    }
}
```

## 学习结束了，给作者来杯咖啡？

{% page-ref page="../../0lemon/coffee.md" %}

