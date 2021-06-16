## Liberty.Finance NFT API
--------
### 1.Pixel销售页面信息（Wayne）
> 1.1 剩余和已销售信息 + Key Metrics信息  

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

输入参数：fromAddress,pixel数量
需要知道合约地址，及其合约方法

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

调用合约方法参数包含：
```json
  {
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "left":100,
        "top":100,
        "width":200,
        "height":100,
        "price":""
    }
```
测试网合约地址:https://ropsten.etherscan.io/address/0x4816118310F1453d3A29Bb9Af17bA3B39dC297c7#code

方法: mint(address to, string memory _tokenURI, uint256 index, uint256 startX, uint256 startY, uint256 xLength, uint256 yLength)
参数:
```json
  {
        "_tokenURI":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "index":0, (广告牌编号 默认值0)
        "startX":100,(NFT左上角x坐标)
        "startY":100,(NFT左上角y坐标)
        "xLength":200,(NFT宽度)
        "yLength":100,(NFT高度)
    }
```
### 3.编辑自己的NFT信息（尔衡/浩洋）

> 3.1上传图片到ipfs接口 (同2.1)

> 3.2上传NFT json数据到ipfs接口 (同2.2)

> 3.3调用合约方法编辑nft（x,y,w,h）这4个值是不可以变的

调用合约方法参数包含：
```json
  {
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "price":""
    }
```
测试网合约地址:https://ropsten.etherscan.io/address/0x4816118310F1453d3A29Bb9Af17bA3B39dC297c7#code

方法: setTokenURI(uint256 tokenId, string memory tokenURI)

### 4.获取全部NFT信息接口（尔衡/浩洋）

> 4.1通过合约中的方法获取所有的NFT信息

输入参数：合约地址
输出：
```json
[
    {
        "id":"0x01",
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "owner":"0x8073dfe92b13efb94f187537008e47fda5215262",
        "left":100,
        "top":100,
        "width":200,
        "height":100,
        "price":"",
        "createTime":1623251669017,
        "updateTime":1623253668161,
        "blur":false,
        "voteCounter":10
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

卖NFT（设置价格,挂单）方法: readyToSellToken(uint256 _tokenId, uint256 _price)
取消卖单 方法: CancelSellToken(uint256 _tokenId)


### 6.NFT市场，可以根据类型筛选（尔衡/浩洋）
> 6.1通过合约中的方法获取所有的NFT信息（同4.1）

> 6.2通过nft.url获取json数据（同4.2） 然后根据json中的类型筛选NFT

> 6.3通过json中的图片url，获取图片（同4.3）



### 7.查询地址的NFT信息（尔衡/浩洋）
> 7.1通过合约中的方法获取address下的所有NFT

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
```json
  {
        "id":"0x01",
        "url":"https://gateway.pinata.cloud/ipfs/QmXQt3AGb2QUzVTGLvXfeg7WJN13GGqiUjM3zL1WvUs3UL",
        "owner":"0x8073dfe92b13efb94f187537008e47fda5215262",
        "left":100,
        "top":100,
        "width":200,
        "height":100,
        "price":"",
        "createTime":1623252461329,
        "updateTime":1623254460473,
        "blur":false,
        "voteCounter":10,
        "history":[
            {
                "event":"name",
                "price":"102",
                "from":"0x8073dfe92b13efb94f187537008e47fda5215262",
                "to":"0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee",
                "date":1623254460474
            }
        ]
    }
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







