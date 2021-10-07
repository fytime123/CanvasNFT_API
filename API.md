## Liberty.Finance NFT API
--------
### 1.Pixel销售页面信息（Wayne）
> 1.1 剩余和已销售信息 + Key Metrics信息  

PIXEL的供用总量：用pixel合约的totalSupply()方法查询    

```javascript
ethereum.request({
  method: 'eth_call',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//钱包地址
      to: '0x7def6961f3c752c83ecf3947deb5c71d65f33426',//Pixel合约地址
      data:'0x18160ddd'
    },
  ],
})
.then((totalRemain) => console.log(totalRemain))
.catch((error) => console.error);
```

可购买的PIXEL余额：用pixel合约的totalRemaining()方法查询  

```javascript
ethereum.request({
  method: 'eth_call',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//钱包地址
      to: '0x7def6961f3c752c83ecf3947deb5c71d65f33426',//Pixel合约地址
      data:'0xd8a54360'
    },
  ],
})
.then((totalRemain) => console.log(totalRemain))
.catch((error) => console.error);
```



从服务端获取数据为：
```json
{
    "pixelRemain":800000,
    "pixelSold":200000,
    "tokenName":"PIXEL",
    "blockchainNetwork":"Binance Smart Chain",
    "price":"1.0",
    "totalSupply":1000000,
    "totalRaise":1000000,
    "maxAllocation":1000,
    "tokenSupport":"BUSD",
    "endTime":1623646870884
}
```

> 1.2购买Pixel合约接口    

第一步：同意授权DAI订购PIXEL  

Function: approve(address usr, uint256 amount)  

MethodID: 0x095ea7b3  

[0]:  0000000000000000000000007def6961f3c752c83ecf3947deb5c71d65f33426    

[1]:  ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff    

```javascript
ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//钱包地址
      to: '0x668de74b03a5b5a370ca189192bb8c63e386bdd4',//DAI 合约地址
data:'0x095ea7b30000000000000000000000007def6961f3c752c83ecf3947deb5c71d65f33426ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);
```

第二步：购买  

Function: purchase(uint256 amount)  

MethodID: 0xefef39a1  

[0]:  0000000000000000000000000000000000000000000000000000000000000064  


```javascript
ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//钱包地址
      to: '0x7def6961f3c752c83ecf3947deb5c71d65f33426',//Pixel合约地址
      data:'0xefef39a10000000000000000000000000000000000000000000000000000000000000064' //订购数量
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);
```   



如果第一步前面已经approve了，可以查询  

查询DAI的ABI方法为：  
```json
{
    "inputs":[
        {
            "internalType":"address",
            "name":"owner",
            "type":"address"
        },
        {
            "internalType":"address",
            "name":"spender",
            "type":"address"
        }
    ],
    "name":"allowance",
    "outputs":[
        {
            "internalType":"uint256",
            "name":"",
            "type":"uint256"
        }
    ],
    "stateMutability":"view",
    "type":"function"
}
```   


js调用方法：  

```javascript

ethereum.request({
  method: 'eth_call',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//我的钱包地址
      to: '0x668de74b03a5b5a370ca189192bb8c63e386bdd4',//dai合约地址
//data第一个参数为我的钱包地址，第二个参数为pixel合约地址
      data:'0xdd62ed3e00000000000000000000000041fea2d4efef108f6495b311dad5e2b21c23b4ee0000000000000000000000007def6961f3c752c83ecf3947deb5c71d65f33426'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```   


### 2.创建NFT接口（尔衡/浩洋）
> 2.1上传图片到ipfs接口  

参考：https://pinata.cloud/documentation#PinFileToIPFS  

image上传成功，得到图片的url

> 2.2上传NFT json数据到ipfs接口  

参考：https://pinata.cloud/documentation#PinJSONToIPFS  

upload json data:
```json
{
    "type":"scenery",
    "title":"Title here for nFT",
    "url":"https://www.google.com",
    "introduction":"The global leader connecting brands with video games, apps, and VR/AR. Epik brings to life unique collaborations inside of digital platforms delivering an experience that users love. ",
    "imageUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
    "imageSketchUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL"
}
```
返回值：
https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL


> 2.3调用合约方法创建nft


测试网合约地址: https://kovan.etherscan.io/address/0xd13c6eaa1fb05b41046c886db46a0131c05f9b68#writeContract
方法: mint(address to, string memory_tokenURI, uint256 startX, uint256 startY, uint256 xLength, uint256 yLength) 参数:
methodId = 0xf382555e  

ABI
```javaScript
{
        "inputs":[
            {
                "internalType":"address",
                "name":"to",
                "type":"address"
            },
            {
                "internalType":"string",
                "name":"_tokenURI",
                "type":"string"
            },
            {
                "internalType":"uint256",
                "name":"startX",
                "type":"uint256"
            },
            {
                "internalType":"uint256",
                "name":"startY",
                "type":"uint256"
            },
            {
                "internalType":"uint256",
                "name":"xLength",
                "type":"uint256"
            },
            {
                "internalType":"uint256",
                "name":"yLength",
                "type":"uint256"
            }
        ],
        "name":"mint",
        "outputs":[

        ],
        "stateMutability":"payable",
        "type":"function"
    }
```
```javaScript

ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',//用户自己的钱包地址
      to: '0xd13c6eaa1fb05b41046c886db46a0131c05f9b68',//创建NFT合约地址
      value:'0x5af3107a4000',//0.0001ETH
      data:'0xf382555e00000000000000000000000041fea2d4efef108f6495b311dad5e2b21c23b4ee00000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c800000000000000000000000000000000000000000000000000000000000000c8000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000022222000000000000000000000000000000000000000000000000000000000000'
      //data的参数 mint("0x41fea2d4efef108f6495b311dad5e2b21c23b4ee",'""',0,200,200,10,10)
      //参考 http://cw.hubwiz.com/card/c/web3.js-1.0/1/7/6/        http://www.jouypub.com/2018/1292c65cfbe128f290fb336d930d3bca/
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);
```

调用合约方法参数包含：
```json
  {
        "memory_tokenURI":"",
        "index": 0,
        "startX":200,
        "startY":200,
        "xLength":10,
        "yLength":10
    }
```


### 3.编辑自己的NFT信息（尔衡/浩洋）

> 3.1上传图片到ipfs接口 (同2.1)

> 3.2上传NFT json数据到ipfs接口 (同2.2)

> 3.3调用合约方法编辑nft（x,y,w,h）这4个值是不可以变的

测试网合约地址:https://ropsten.etherscan.io/address/0x8a78d7013703d45947d6710449825697677b0342#code

canvasContract.approve(nftContractAddress,-1)
```javaScript
 ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',
      to: '0x7de10783fd90e9351aff82dcf3ef2538139536ae',//canvas合约地址  或者 DAI合约地址
data:'0x095ea7b3000000000000000000000000d13c6eaa1fb05b41046c886db46a0131c05f9b68ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```


方法: setTokenURI(uint256 tokenId, string memory tokenURI, bool fraud,bool nsfw) fraud、nsfw传flase
methodId = 0x7f908285

```javaScript
{
        "inputs":[
            {
                "internalType":"uint256",
                "name":"tokenId",
                "type":"uint256"
            },
            {
                "internalType":"string",
                "name":"_tokenURI",
                "type":"string"
            },
            {
                "internalType":"bool",
                "name":"fraud",
                "type":"bool"
            },
            {
                "internalType":"bool",
                "name":"nsfw",
                "type":"bool"
            }
        ],
        "name":"setTokenURI",
        "outputs":[

        ],
        "stateMutability":"nonpayable",
        "type":"function"
    }
```

```javaScript
 ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',
      to: '0xd13c6eaa1fb05b41046c886db46a0131c05f9b68',// NFT合约地址
data:'0x7f908285000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005068747470733a2f2f676174657761792e70696e6174612e636c6f75642f697066732f516d564a4746354d73476b59426544634c78474553534e36653559506258346f466f4d6936487a356f4b3461526900000000000000000000000000000000'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);


```

调用合约方法参数包含：
```json
  {
       "memory_tokenURI":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
       "index": 552
  }
```


### 4.获取全部NFT信息接口（尔衡/浩洋）

> 4.1通过合约中的方法获取所有的NFT信息 ***(价格信息怎么获取？？？？？？？)*** ==>参看（10.1 第2条）

访问Subgraph:  https://api.studio.thegraph.com/query/7102/zubertest_canvasnft/v0.12.0_kovan
Example Query:
```graphql
{
  canvasNFTInfos{
              id
              tokenId
              owner
              startX
              startY
              xLength
              yLength
              createTime
              updateTime
              fraud
              nsfw
              tokenURI
          }
}
```

输出：
```json
[
    {
        "id":"0x01",
        "tokenId":"0x017889",
        "index":"0x122",
        "startX":100,
        "startY":100,
        "xLength":200,
        "yLength":100,
        "createTime":1623251669017,
        "updateTime":1623253668161,
        "blur":false,
        "govCounter":10,
        "unsafe": true,
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "owner":"0x8073dfe92b13efb94f187537008e47fda5215262"
    }
]
```

> 4.2通过nft.url获取nft信息json数据
```json
{
    "type":"scenery",
    "title":"Title here for nFT",
    "url":"https://www.google.com",
    "introduction":"The global leader connecting brands with video games, apps, and VR/AR. Epik brings to life unique collaborations inside of digital platforms delivering an experience that users love. ",
    "imageUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
    "imageSketchUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL"
}
```

> 4.3通过json中的图片url，获取图片



### 5.购买NFT（尔衡/浩洋）
输入参数：nft.id,fromAddress,合约地址

测试网合约地址:  https://ropsten.etherscan.io/address/0x941CbE144eE720Cf99A37ab2eFD738148D517685#code
购买NFT 方法：buyToken(uint256 _tokenId)
methodId = 0x2d296bf1

busdContract.approve(bidNFTContractAddress,-1)  

Function: approve(address spender, uint256 amount)  

```javaScript

ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0xf72aa81038ce6170ae5041058597fd98af7ced44',//用改钱包地址购买
      to: '0x7de10783fd90e9351aff82dcf3ef2538139536ae',//DAI合约地址
data:'0x095ea7b3000000000000000000000000c81c4ed318ccc96c3ade6d27c02bf647ddd5e1fbffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```


Function: buyToken(uint256 _tokenId)  

```javaScript

 ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0xf72aa81038ce6170ae5041058597fd98af7ced44',//用改钱包地址购买
      to: '0xc81c4ed318ccc96c3ade6d27c02bf647ddd5e1fb',//bidNFT Contract Address
data:'0x2d296bf10000000000000000000000000000000000000000000000000000000000000004'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```



卖NFT（设置价格,挂单）方法: readyToSellToken(uint256 _tokenId, uint256 _price)
methodId = 0x523a57cf

NFTContract.approve(bidContractAddress,tokenId)  

Function: approve(address to, uint256 tokenId)  

```javaScript

 ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',
      to: '0xd13c6eaa1fb05b41046c886db46a0131c05f9b68',// NFTContract address
data:'0x095ea7b3000000000000000000000000c81c4ed318ccc96c3ade6d27c02bf647ddd5e1fb0000000000000000000000000000000000000000000000000000000000000004'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```

readyToSellToken(uint256 _tokenId, uint256 _price)  

```javaScript

 ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',
      to: '0xc81c4ed318ccc96c3ade6d27c02bf647ddd5e1fb',//bid NFT cotract Address
data:'0x523a57cf00000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000006bc75e2d63100000'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```


取消卖单 方法: CancelSellToken(uint256 _tokenId)
methodId = 0x9a9d9a5a


```javaScript

ethereum.request({
  method: 'eth_sendTransaction',
  params: [
    {
      from: '0x41fea2d4efef108f6495b311dad5e2b21c23b4ee',
      to: '0xc81c4ed318ccc96c3ade6d27c02bf647ddd5e1fb',//bid NFT cotract Address
data:'0xb84eb76a0000000000000000000000000000000000000000000000000000000000000004'
    },
  ],
})
.then((txHash) => console.log(txHash))
.catch((error) => console.error);

```



### 6.NFT市场，可以根据类型筛选（尔衡/浩洋）
> 6.1通过合约中的方法获取所有的NFT信息（同4.1）

> 6.2通过nft.url获取json数据（同4.2） 然后根据json中的类型筛选NFT

> 6.3通过json中的图片url，获取图片（同4.3）



### 7.查询地址的NFT信息（尔衡/浩洋）
> 7.1通过合约中的方法获取address下的所有NFT
访问Subgraph:  https://api.studio.thegraph.com/query/7102/zubertest_canvasnft/v0.12.0_kovan
Example Query:
```graphql
{
  canvasNFTInfos(where: { owner: "0x799621c508498bb0a6482b6596a3a2e908bcbbba" }){
                id
                tokenId
                owner
                startX
                startY
                xLength
                yLength
                createTime
                updateTime
                fraud
                nsfw
                tokenURI
  }
}
```
输出：
```json
[
    {
        "id":"0x01",
        "tokenId":"0x017889",
        "index":"0x122",
        "startX":100,
        "startY":100,
        "xLength":200,
        "yLength":100,
        "createTime":1623251669017,
        "updateTime":1623253668161,
        "blur":false,
        "govCounter":10,
        "unsafe": true,
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "owner":"0x8073dfe92b13efb94f187537008e47fda5215262"
    }
]
```


> 7.2通过nft.url获取json数据（同4.2）

> 7.3通过json中的图片url，获取图片（同4.3）




### 8.canvas余额，pixel余额（Wayne）



### 9.挖矿接口（Wayne）
> 9.1获取当前矿池apy  
从服务端获取数据：
```json
{
    "currentCANVASPrice":"1.0",
    "totalValueLocked":"123456789",
    "circulatingCANVAS":"100000.0",
    "pools":[
        {
            "poolName":"CANVAS-BNB POOL",
            "iconUrl":"https://xxxxx.com/icon/bnbPool.jpg",
            "introduction":"We encourge hodlers to stake their LP token to earn more CANVAS.Simply add CANVAS-BNB LP via Pancakeswap",
            "apr":"600.0",
            "tvl":"310006000",
            "stakedBalance":"1000.0",
            "earnedCANVAS":"2.0"
        },
        {
            "poolName":"CANVAS-BUSD POOL",
            "iconUrl":"https://xxxxx.com/icon/BUSDPool.jpg",
            "introduction":"We encourge hodlers to stake their LP token to earn more CANVAS.Simply add CANVAS-BUSD LP via Pancakeswap",
            "apr":"600.0",
            "tvl":"385006000",
            "stakedBalance":"1000.0",
            "earnedCANVAS":"2.0"
        },
        {
            "poolName":"CANVAS POOL",
            "iconUrl":"https://xxxxx.com/icon/BUSDPool.jpg",
            "introduction":"We encourge hodlers to stake their LP token to earn more CANVAS.Simply add CANVAS LP via Pancakeswap",
            "apr":"510.0",
            "tvl":"39610600",
            "stakedBalance":"1000.0",
            "earnedCANVAS":"2.0"
        }
    ]
}
```

> 9.2抵押代币

> 9.3提取抵押代币





### 10.获取nft.id的详情，包括历史交易信息（尔衡/浩洋）
> 10.1 通过ID，获取NFT链上数据详情

分两个subgraph query
1）、NFT的属性查询
访问Subgraph:  https://thegraph.com/subgraphs/name/erhenglu/libertynft
Example Query:
```graphql
{
  canvasNFTs(where: { tokenId: 2}){
    id
    tokenId
    index
    startX
    startY
    xLength
    yLength
	createTime
	updateTime
	blur
	govCounter
	unsafe
	url
	owner
  }
}
```
返回结果：
```json
{
    "id":"0x01",
    "tokenId":"0x017889",
    "index":"0x122",
    "startX":100,
    "startY":100,
    "xLength":200,
    "yLength":100,
    "createTime":1623251669017,
    "updateTime":1623253668161,
    "blur":false,
    "govCounter":10,
    "unsafe": true,
    "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
    "owner":"0x8073dfe92b13efb94f187537008e47fda5215262"
}
```


2）、NFT价格和历史记录查询 
访问Subgraph: https://thegraph.com/explorer/subgraph/erhenglu/libertymarket
价格 Example query:
```graphql
{
  canvasNFTs(where: { tokenId: 2}){
    id
    tokenId
    price
    seller
    onSale 
  }
}
```
返回结果：
```json
{
    "id":"0x01",
    "tokenId":"0x017889",
    "price": "0x455255",
    "seller":"0x8073dfe92b13efb94f187537008e47fda5215262",
    "onSale":54566
}
```
onSale=true说明正在挂单售卖
onSale=false说明这个NFT没有挂单



3）、交易记录 Example query:
```graphql
{
  tradeHistories(where: { tokenId: 2}){
    id
    tokenId
    price
    seller
    buyer
    fee
    blockId
    time
  }
}
```
返回结果：
```json
[
    {
        "id":"0x01",
        "tokenId":"0x017889",
        "price": "0x455255",
        "seller":"0x8073dfe92b13efb94f187537008e47fda5215262",
        "buyer":"0x799621c508498bb0a6482b6596a3a2e908bcbbba",
        "fee":788,
        "blockId":"0x4855755",
        "time": 1623253668161
    }
]
```


> 10.2通过url获取NFT信息json
```json
{
    "type":"scenery",
    "title":"Title here for nFT",
    "url":"https://www.google.com",
    "introduction":"The global leader connecting brands with video games, apps, and VR/AR. Epik brings to life unique collaborations inside of digital platforms delivering an experience that users love. ",
    "imageUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
    "imageSketchUrl":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL"
}
```


### 11.用户投票要求隐藏图片显示


### 12.用户的favorite（Wayne）
>  12.1市场中favorite数据获取  

>  12.2用户地址的favorite数据获取  




### 13.空投合约




### 附录
####  1.测试合约地址
+ Pixel合约地址  

0x7def6961f3c752c83ecf3947deb5c71d65f33426  //0xb59efd0f19fb9e9cb32d3e84bebec5ca4144c95e

+ Canvas合约地址  

//0xcd5a398f67b95670caf38f58078719419ab9ee0e

+ 创建NFT合约地址（LibertyNFT）  

0x986b5587960b1512804421ad33305833e9327137    //0xd13c6eaa1fb05b41046c886db46a0131c05f9b68      //0xa770814c47f42c86ae52f33428dc9a042429e5d9    //0x8a78d7013703d45947d6710449825697677b0342

+ BidNFT  

0xac5bceae6b7e4184019d6305e3d4fdd57325c4c1   //0xc81c4ed318ccc96c3ade6d27c02bf647ddd5e1fb     //0x3573846c388e009ac8d5e89edf2523efa6f04d3f   //0xa7222b1d61facf5fe59c07363fef4345b537f1a9

+ 空投合约地址  

？

+ 购买Pixel合约地址  

？

+ 旷池合约地址  

？

+ DAI合约地址  

0x7de10783fd90e9351aff82dcf3ef2538139536ae    //0x668de74b03a5b5a370ca189192bb8c63e386bdd4   //0x01d72303e276bc4535519af73c1be4d51656c1c4


####  2.正式合约地址






