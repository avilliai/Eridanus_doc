---
sidebar_position: 1
---
# 部署
后续会发布专门的部署工具

# 配置
## Eridanus配置
config/basic_config.yaml
```yaml
bot:
  name: "Eridanus"
master:
  name: "主人"
  id: 1840094972
adapter:
  access_token: "any_access_token" #onebot实现部分为空则不用改
  http_sever:       #bot的运行端口，onebot的事件上报到这里
    host: "0.0.0.0"
    port: 8080
  http_client:
    url: "http://127.0.0.1:3000"  #bot发送的http请求地址。即onebot实现的http sever地址
  ws_client:
    ws_link: "ws://127.0.0.1:3001"  #bot的websocket请求地址
```
一般来说，改改bot的名字和master信息得了。剩下都是onebot默认配置。
## onebot实现部分
使用http适配器时，需要同时开启onebot实现的http服务端功能和http客户端功能。

ws适配器没做完。
### 以napcat为例
![img.png](核心功能/img/img.png)
`点添加配置时，不要忘了点击【启用。】`

如上图，onebot实现的http服务器在3000端口

而上报地址为
```yaml
http://localhost:8080
```
### 以llob为例
![img.png](核心功能/img/llob.png)

