## Liberty.Finance NFT API
--------
#### 1.购买Pixel合约接口
输入参数：fromAddress,pixel数量
需要知道合约地址，及其合约方法

#### 2.创建NFT接口
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


#### 3.编辑自己的NFT信息

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


#### 4.获取全部NFT信息接口

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



#### 5.购买NFT
输入参数：nft.id,fromAddress,合约地址



#### 6.NFT市场，可以根据类型筛选
> 6.1通过合约中的方法获取所有的NFT信息（同4.1）

> 6.2通过nft.url获取json数据（同4.2） 然后根据json中的类型筛选NFT

> 6.3通过json中的图片url，获取图片（同4.3）



#### 7.查询地址的NFT信息
> 7.1通过合约中的方法获取address下的所有NFT

> 7.2通过nft.url获取json数据（同4.2）

> 7.3通过json中的图片url，获取图片（同4.3）




#### 8.canvas余额，pixel余额



#### 9.挖矿接口
> 9.1抵押代币

> 9.2提取抵押代币

> 9.3获取当前矿池apy



#### 10.获取nft.id的详情，包括历史交易信息
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


#### 11.用户投票要求隐藏图片显示





