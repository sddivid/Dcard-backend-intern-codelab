# ㄔㄡCard 的 docker-compose Codelab

## Prerequisites
確保目錄下有兩個相依的 submodule
```
git clone https://github.com/CS6/D4-homework-Frontend.git
git clone https://github.com/CS6/D4-homework-Backend.git
```

## How To Run
```shell
docker-compose up 
```

## How To Delet Dangling Images
[移除最近1小時產生的 Dangling Images](https://docs.docker.com/engine/reference/commandline/image_prune/)
```dockerfile
docker image prune -a --filter "until=1h"
```

## How To Delet jmeter compose
```shell
rm -rf ${PWD}/jmeter/compose
```
## How To Edit jmeter Test Plen
jmeter GUI Open the
```shell
${PWD}/jmeter/http-request-test.jmx
```

## How To Edit haproxy.cfg
jmeter GUI Open the
```shell
${PWD}/haproxy/haproxy.cfg
```
# 互動測試架構

![互動測試架構](https://github.com/CS6/docker-codelab/blob/4e5ec4ba215464aca041affb7a738afe8427fd67/img/Flow.png)

{ Jmeter_F2E } HAhaproxy => Frontend{ Jmeter Docker } => Backend => DB[redis,mongo]

使用者 或是 jmeter GUI 請求Frontend頁面 (haproxy 限制流量)
請求Frontend頁面 或是 jmeter Docker 請求Backend (Redis+lua 限制流量)

#### jmeter 容器的作用？
模擬來自多客戶端 IP 對後端的請求




## `注意` ： 這邊理論上不該開放外部存取 Port ， 用於實際環境請記得關閉並透過 networks 建立



https://drive.google.com/file/d/1tZ2m3xwh_hDqq0sKWJsSvVBCzts1ZrzG/view?usp=sharing
| services             |   角色   |                       功能 |  Port |
|----------------------|:--------:|---------------------------:|------:|
| haproxy-dcard        |   代理   |         代理前端與限制流量 |    80 |
| carddrawcardfrontend |   前端   |               顯示抽卡資料 |    80 |
| dcarddrawcardbackend |   後端   | 提供抽卡資料＆抽卡次數限制 |  3000 |
| redis-server         |    DB    |           紀錄抽卡次數限制 |  6379 |
| mongo                |    DB    |               紀錄抽卡資料 | 27017 |
| jmeter-master        | 測試工具 |               請求次數測試 |  jmeter-net |
| jmeter--slave-1      | 測試工具 |               請求次數測試 | jmeter-net |
| jmeter--slave-2      | 測試工具 |               請求次數測試 | jmeter-net |
| jmeter--slave-3      | 測試工具 |               請求次數測試 | jmeter-net |




#＃ 互動測試結果
![互動測試結果](https://github.com/CS6/docker-codelab/blob/4e5ec4ba215464aca041affb7a738afe8427fd67/img/JMeter.png)

#＃ jmeter 給予 1500 次請求之結果 
<img width="1538" alt="image" src="https://user-images.githubusercontent.com/13188949/113802431-4fcdc380-978d-11eb-945e-f359cd6c0d24.png">



HA => F2E => B2E => DB[redis,mongo]



{jmeter_F2E(GUI)}HA => F2E{jmeter_M} => B2E => {Robo3T(GUI),ARDM(GUI)}DB[redis,mongo]


