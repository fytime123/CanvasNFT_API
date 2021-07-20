1.Restful API接口
1.1获取图片和NFT信息最新更新时间
http://host/nftcanvas/canvas_time

result:
```json
{
    "code": 0,
    "data":{"updateTime":1626773446308,"url":"http://waitImageUrl"}
}
```


1.2获取NFT信息
获取分类为5的NFT
http://host/nftcanvas/nft?type=5
```json
{
    "code": 0,
    "data": [
        {
            "contract": {
                "id": "0x5",
                "tokenId": "5",
                "startX": 210,
                "startY": 210,
                "xLength": 10,
                "yLength": 10,
                "createTime": "1625499531",
                "updateTime": "1625836557",
                "blur": false,
                "govCounter": 0,
                "unsafe": false,
                "url": "https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                "owner": "0xed6d69fda578f7f7ec361115c10d1a91165dd7e3"
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

获取所有的NFT
http://host/nftcanvas/nft?type=   





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
            "contract":{
                "id":"0x5",
                "tokenId":"5",
                "startX":210,
                "startY":210,
                "xLength":10,
                "yLength":10,
                "createTime":"1625499531",
                "updateTime":"1625836557",
                "blur":false,
                "govCounter":0,
                "unsafe":false,
                "url":"https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                "owner":"0xed6d69fda578f7f7ec361115c10d1a91165dd7e3"
            },
            "user":{
                "id":28,
                "type":"5",
                "title":"jack测试token",
                "url":"http://saying-tech.cn",
                "imageUrl":"https://gateway.pinata.cloud/ipfs//QmYCVqGworCiUPCQDYe6xzaZoLaA9m6mDHFm8NArec77gs",
                "introduction":"测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试"
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
            "contract":{
                "id":"0x5",
                "tokenId":"5",
                "startX":210,
                "startY":210,
                "xLength":10,
                "yLength":10,
                "createTime":"1625499531",
                "updateTime":"1625836557",
                "blur":false,
                "govCounter":0,
                "unsafe":false,
                "url":"https://gateway.pinata.cloud/ipfs/QmVJGF5MsGkYBeDcLxGESSN6e5YPbX4oFoMi6Hz5oK4aRi",
                "owner":"0xed6d69fda578f7f7ec361115c10d1a91165dd7e3"
            },
            "user":{
                "id":28,
                "type":"5",
                "title":"jack测试token",
                "url":"http://saying-tech.cn",
                "imageUrl":"https://gateway.pinata.cloud/ipfs//QmYCVqGworCiUPCQDYe6xzaZoLaA9m6mDHFm8NArec77gs",
                "introduction":"测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试测试"
            }
        }
    ],
    "type":"nft"
}
```   