# 表现

```go
db.getSiblingDB("jarvis").getCollection("nodeEarn")
                  .find({_id: "62bf6e60f269760254161bb9"})
                  .limit(201)
```
数据库中有记录 _id:62bf6e60f269760254161bb9的数据存在,但是就是查不出来

[解决方案](https://stackoverflow.com/questions/24427845/can-not-find-a-record-by-its-id-in-mongodb)

```go
 db.getSiblingDB("jarvis").getCollection("nodeEarn")
          .find({_id: ObjectId("62bf6e60f269760254161bb9")})
          .limit(201)
```

本地脚本`go build`之后在线上运行不起来,可能的原因是mac和linux版本不匹配

```go
➜  nodehistorydetail git:(yanzezhong/1919) env GOOS=linux GOARCH=amd64 go build -v main.go                          
```
[解决方案](https://stackoverflow.com/questions/36198418/golang-cannot-execute-binary-file-exec-format-error)
[详细了解](https://dave.cheney.net/2015/08/22/cross-compilation-with-go-1-5)
用这个命令进行编译,然后丢到跳板机执行.

db.getSiblingDB("jarvis").getCollection("nodeEarn").find({curDayPeak95:{"$gt":0}}).limit(1001)

向跳板机发布

scp main  yanzezhong@10.20.34.27:~/


寻找计量数据

curl -XPOST http://defy-csapi.qiniu.io/v2/pcdn/node/avg95 -d '{ "deviceIds":["38195790445b61779864af1970df1080"], "nodeType": "standalone", "start":"2022-09-01", "end":"2022-10-01", "vendor": 1811031131 }' -H "Content-Type: application/json" | jq .


curl -XPOST http://pcdntraffic.defy.internal.qiniu.io/v2/pcdn/node/avg95 -d '{ "deviceIds":["75a93ce7e1d83c872c00000000000001"], "start":"2022-09-01", "end":"2022-10-01", "vendor": 389 }' -H "Content-Type: application/json" | jq .

登录跳板机

qssh xs3307


如何拉取PR

https://blog.csdn.net/April_Lie/article/details/106554769

准备工作

https://github.com/selfteaching/the-craft-of-selfteaching/issues/67





curl --location --request GET 'https://jarvis-apigate-inner-v2.niulinkcloud.com/api/proxy/jarvis/v1/nodes/base' \
--header 'Authorization: QBox f792033b3449b484819864218fd2b941:gO9xnYKuLS_OgTwCYyltYkDls9U' \
--header 'Content-Type: application/json' \
--data-raw '{
    "start": 1662037639000,
    "end": 1664543239000,
    "nodeIds": ["b89ba3ef82ed4c149edd2267f68241d0"],
    "customerId": 1380460970
}'


curl --location --request GET 'https://jarvis-apigate-inner-v2.niulinkcloud.com/v1/nodes/base/customer' \
--header 'Authorization: Qiniu f792033b3449b484819864218fd2b941:DsH7i1p0Wfa2YCVrLdcWivqyGP4='




curl --location --request POST 'http://linkcloud-env-dev-admin.qa.qiniu.io/api/proxy/jarvis/v1/nodes/base/customer' \
--header 'Authorization: qZfRazTZTMzZ2GC8njVF0eQ2SkwwMxFxQmXiuh2X:Og7XCEyAYLtm7U-GKDDEXtJLGIE=:eyJob3N0IjoibGlua2Nsb3VkLWVudi1kZXYtYWRtaW4ucWEucWluaXUuaW8iLCJleHBpcmUiOjE2NjY1NzcyNjUsImVtYWlsIjoiIn0=' \
--header 'Content-Type: application/json' \
--data-raw '{
    "start": 1662037639,
    "end": 1664543239,
    "nodeIds": ["200061b01a98b7fe013eaa90578f5110"],
    "customerId": 1380460970
}'


curl --location --request POST 'http://linkcloud-env-dev-admin.qa.qiniu.io/api/proxy/jarvis/v1/nodes/base/customer' \
--header '' \
--header 'Content-Type: application/json' \
--data-raw '{
    "start": 1662037639000,
    "end": 1664543239000,
    "nodeIds": ["c3344e87df76227e0d91189f701d3f60"],
    "customerId": 1380460970
}'


{"10000000":{"userID":10000000,"signID":10000000,"name":"腾讯汇聚","dnsList":["119.29.29.29","114.114.114.114"],"featureCtl":{"mounter":true},"createAt":"2022-10-31T12:36:30.955Z","updateAt":"2022-10-13T12:36:30.955Z"},"10000003":{"userID":10000003,"signID":10000003,"name":"百度XCDN","featureCtl":{"mounter":false},"createAt":"2022-10-31T12:37:30.955Z","updateAt":"2022-10-13T12:37:30.955Z"},"1380317970":{"userID":1380317970,"signID":1380317970,"name":"快手点播","externName":"短视频A","dnsList":["119.29.29.29","180.76.76.76","223.5.5.5"],"featureCtl":{"mounter":true},"createAt":"2022-03-13T05:58:53.014Z","updateAt":"2022-03-13T05:58:53.014Z"},"1380389889":{"userID":1380389889,"signID":1380389889,"name":"爱奇艺盒子","featureCtl":{"mounter":false},"createAt":"2022-09-22T12:04:30.955Z","updateAt":"2022-09-22T22:14:30.955Z"},"1380460970":{"userID":1380460970,"signID":1380460970,"name":"七牛CDN","externName":"业务Q","featureCtl":{"mounter":false},"createAt":"2022-05-24T07:49:27.955Z","updateAt":"2022-05-24T07:49:27.955Z"},"1381044116":{"userID":1381044116,"signID":1381044116,"name":"B站","externName":"长视频B","dnsList":["119.29.29.29","180.76.76.76","223.5.5.5"],"featureCtl":{"mounter":false},"createAt":"2022-03-13T05:58:44.417Z","updateAt":"2022-03-13T05:58:44.417Z"},"1381526443":{"userID":1381526443,"signID":1381526443,"name":"爱奇艺","externName":"长视频A","dnsList":["119.29.29.29","114.114.114.114"],"featureCtl":{"mounter":false},"createAt":"2022-04-27T05:58:44.417Z","updateAt":"2022-04-27T05:58:44.417Z"},"1381989696":{"userID":1381989696,"signID":1381989696,"name":"网聚云联","featureCtl":{"mounter":false},"createAt":"2022-09-20T03:43:30.955Z","updateAt":"2022-09-20T03:43:30.955Z"},"1382490022":{"userID":1382490022,"signID":1382490022,"name":"快手盒子","featureCtl":{"mounter":true},"createAt":"2022-10-13T01:51:30.955Z","updateAt":"2022-10-13T01:51:30.955Z"},"1382522065":{"userID":1382522065,"signID":1382522065,"name":"字节汇聚","featureCtl":{"mounter":false},"createAt":"2022-08-18T12:24:30.955Z","updateAt":"2022-08-18T12:24:30.955Z"},"1382573903":{"userID":1382573903,"signID":1382573903,"name":"渠道腾讯","externName":"业务T","dnsList":["119.29.29.29","114.114.114.114"],"featureCtl":{"mounter":true},"createAt":"2022-03-13T05:58:57.052Z","updateAt":"2022-03-13T05:58:57.052Z"},"1382620146":{"userID":1382620146,"signID":1382620146,"name":"白山","externName":"业务X","featureCtl":{"mounter":true},"createAt":"2022-04-27T05:58:44.417Z","updateAt":"2022-04-27T05:58:44.417Z"},"1382649737":{"userID":1382649737,"signID":1382649737,"name":"直销腾讯","externName":"业务T","dnsList":["119.29.29.29","114.114.114.114"],"featureCtl":{"mounter":true},"createAt":"2022-03-13T05:59:01.072Z","updateAt":"2022-03-13T05:59:01.072Z"},"1382680008":{"userID":1382680008,"signID":1382680008,"name":"字节专线","featureCtl":{"mounter":false},"createAt":"2022-07-15T07:49:27.955Z","updateAt":"2022-08-18T12:24:27.955Z"}}

{}

{"3fd875c4230dafdfb700000000000001":{}}{"3fd875c4230dafdfb700000000000001":{"_id":"63195335a12598b51477dc41","nodeID":"3fd875c4230dafdfb700000000000001","state":"complete","customerID":1380317970,"customerIds":[1380317970],"businessID":"3fd875c4230dafdfb700000000000001","businessIds":["3fd875c4230dafdfb700000000000001"],"desc":"migrate, isStock(true)","createAt":"2022-09-08T02:28:05.634Z","updateAt":"2022-09-08T02:28:05.634Z","lastUpdateNano":1667455848990923225}