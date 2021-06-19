## 钱包接口

### 1.连接到 MetaMask 钱包
检测是否安装？没有安装，去安装  

安装了，链接钱包，获取钱包地址  

参考代码：
https://docs.metamask.io/guide/create-dapp.html#project-setup  

### 2.定义应用程序的图标
当您的站点向 MetaMask 用户发出登录请求时，MetaMask 可能会呈现显示您站点图标的模式。
参考文档：
https://docs.metamask.io/guide/defining-your-icon.html

### 3.向用户注册token
https://docs.metamask.io/guide/registering-your-token.html

### 4.如果您想在地址更改时收到通知
https://docs.metamask.io/guide/accessing-accounts.html

### 5.发送交易
https://docs.metamask.io/guide/sending-transactions.html#example

### 6.合约方法
Ethereum JSON-RPC Methods
For the Ethereum JSON-RPC API, please see the Ethereum wiki (opens new window).

Important methods from this API include:

eth_accounts(opens new window)
eth_call(opens new window)
eth_getBalance(opens new window)
eth_sendTransaction(opens new window)
eth_sign(opens new window)

> 6.1查询token余额:  

获取代币的余额，要通过rpc接口得到接口为：eth_call
查看：https://eth.wiki/json-rpc/api   eth_call
参数
object字段：

from: 钱包地址
to: 代币地址（智能合约地址）
data：0x70a08231000000000000000000000000b60e8dd61c5d32be8058bb8eb970870f07233155
data数据格式：最前边的“0x70a08231000000000000000000000000”是固定的，后边的是钱包地址（不带“0x”前缀）

QUANTITY|TAG，”latest”, “earliest” or “pending”


//Keccak-256("balanceOf(address)")="0x70a08231b98ef4ca268c9cc3f6b4590e4bfec28280db06bb5d45e689f2a360be"
//取前4个字节：0x70a08231
//参考：
//1.https://www.4byte.directory/signatures/?bytes4_signature=0x70a08231

String methodId = "0x70a08231";
data = methodId + "000000000000000000000000" + walletHex;

> 6.2查询token symbol名称:  

//Keccak-256("symbol()")="0x95d89b41e2f5f391a79ec54e9d87c79d6e777c63e32c28da95b4e9e4a79250ec"
//取前4个字节：0x95d89b41
//参考：
//1.https://www.4byte.directory/signatures/

>  6.3查询token decimals:

//Keccak-256("decimals()")="0x313ce567add4d438edf58b94ff345d7d38c45b17dfc0f947988d7819dca364f9"
//取前4个字节：0x313ce567
//参考：
//1.https://www.4byte.directory/signatures/

