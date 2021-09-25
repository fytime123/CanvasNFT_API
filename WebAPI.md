1.Restful API接口
1.1获取图片和NFT信息最新更新时间
http://host/nftcanvas/api/canvas_time

GET方法

result:
```json
{
    "code": 0,
    "data":{"updateTime":1626773446308,"url":"http://waitImageUrl"}
}
```


1.2获取NFT信息
获取分类为5的NFT
http://host/nftcanvas/api/nft
POST方法：

```json
{
  "address":"0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee",//有钱包地址，获取到的NFT信息中isMyFavorite对该钱包查询出来的，没有钱包地址isMyFavorite=false
  "type":"5"//NFT分类type，不填该字段，获取全部NFT（user字段中的type对应）
}
```  
响应结果
```json
{
    "code": 0,
    "data": [
        {
            "contract": {
                "id": "0x1",
                "tokenId": "1",
                "startX": 100,
                "startY": 0,
                "xLength": 100,
                "yLength": 100,
                "createTime": "1631606276",
                "updateTime": "1631606276",
                "nsfw": false,
                "tokenURI": "https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                "owner": "0x54e44632a6eab63fa82a9b8a222911cf02f486f0",
                "favoriteCount": 0,//收藏数量
                "voteCount": 0,//投票数量
                "myFavorite": false //0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee该用户是否收藏
            },
            "user": {
                "id": 28,
                "type": "5",
                "title": "jack测试token",
                "url": "http://saying-tech.cn",
                "imageUrl": "https://gateway.pinata.cloud/ipfs//QmYCVqGworCiUPCQDYe6xzaZoLaA9m6mDHFm8NArec77gs",
                "introduction": "测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试"
            }
        }
    ]
}
```   

1.3 获取创建NFT的ETH费用
http://host/nftcanvas/api/createNftPrice

GET方法

result:
```json
{
    "code": 0,
    "data":{"price":"0.0001"}
}
```

1.4 用户收藏关注NFT（favorite），先钱包签名，然后提交到服务端接口
http://host/nftcanvas/api/sign

POST方法
request
```json
{
    "signType": "favorite", 
    "signature": "0xcc9418a65d9f7578d997e0ef52c2c10a583d51176333c11c60e8437b0159ed5a11f7b3ba1d8a8a64b07986d248d3f961e388f9a34748b1b03993c87b81cda2d71c", 
    "message": "{\"favorite\":true,\"tokenId\":\"4\"}", 
    "address": "0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee", 
    "tokenId": "4"
}
```
收藏成功
result:
```json
{
    "code": 0,//收藏成功为0，否则为其他值
    "data":true
}
```



1.5 用户投票投诉NFT，先钱包签名，然后提交到服务端接口
http://host/nftcanvas/api/sign

POST方法
request
```json
{
    "signType": "vote", 
    "signature": "0xcc9418a65d9f7578d997e0ef52c2c10a583d51176333c11c60e8437b0159ed5a11f7b3ba1d8a8a64b07986d248d3f961e388f9a34748b1b03993c87b81cda2d71c", 
    "message": "{\"vote\":1,\"tokenId\":\"4\"}", 
    "address": "0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee", 
    "tokenId": "4"
}
```
投票成功
result:
```json
{
    "code": 0,//收藏成功为0，否则为其他值
    "data":true
}
```


2.WebSocket接口
2.1获取图片和NFT信息最新更新时间
request:
```json
{"type":"canvasImageInfo"}
```   

result:
```json
{"code":0,"data":{"updateTime":1626773446308,"url":"http://waitImageUrl"},"type":"canvasImageInfo"}
```   

2.2获取NFT信息
获取分类为5的NFT
request:
```json
{"type":"nft","data":"5"}
```   

result:
```json
{
    "code":0,
    "data":[
        {
            "contract": {
                        "id": "0x1",
                        "tokenId": "1",
                        "startX": 100,
                        "startY": 0,
                        "xLength": 100,
                        "yLength": 100,
                        "createTime": "1631606276",
                        "updateTime": "1631606276",
                        "nsfw": false,
                        "tokenURI": "https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                        "owner": "0x54e44632a6eab63fa82a9b8a222911cf02f486f0",
                        "favoriteCount": 0,//收藏数量
                        "voteCount": 0,//投票数量
                        "myFavorite": false //0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee该用户是否收藏
                    },
            "user": {
                "id": 28,
                "type": "5",
                "title": "jack测试token",
                "url": "http://saying-tech.cn",
                "imageUrl": "https://gateway.pinata.cloud/ipfs//QmYCVqGworCiUPCQDYe6xzaZoLaA9m6mDHFm8NArec77gs",
                "introduction": "测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试"
            }
        }
    ],
    "type":"nft"
}
```   



获取所有,data参数
request:
```json
{"type":"nft"}
```   

result:
```json
{
    "code":0,
    "data":[
        {
            "contract": {
                        "id": "0x1",
                        "tokenId": "1",
                        "startX": 100,
                        "startY": 0,
                        "xLength": 100,
                        "yLength": 100,
                        "createTime": "1631606276",
                        "updateTime": "1631606276",
                        "nsfw": false,
                        "tokenURI": "https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                        "owner": "0x54e44632a6eab63fa82a9b8a222911cf02f486f0",
                        "favoriteCount": 0,//收藏数量
                        "voteCount": 0,//投票数量
                        "myFavorite": false //0x41fEa2D4eFEF108F6495B311daD5E2B21C23b4Ee该用户是否收藏
                     },
            "user": {
                "id": 28,
                "type": "5",
                "title": "jack测试token",
                "url": "http://saying-tech.cn",
                "imageUrl": "https://gateway.pinata.cloud/ipfs//QmYCVqGworCiUPCQDYe6xzaZoLaA9m6mDHFm8NArec77gs",
                "introduction": "测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试"
            }
        }
    ],
    "type":"nft"
}
```   