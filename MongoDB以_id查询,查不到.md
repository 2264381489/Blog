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