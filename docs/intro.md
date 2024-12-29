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
**ws适配器和http适配器二选一。**

使用ws适配器时，需要开启onebot实现的正向websocket服务。

使用http适配器时，需要同时开启onebot实现的http服务端功能和http客户端功能。
### 以napcat为例
![img.png](核心功能/img/img.png)
`点添加配置时，不要忘了点击【启用】`
#### 使用ws适配器
如上图最右侧，开启了ws服务器，端口为3001
#### 使用http适配器
如上图，onebot实现的http服务器在3000端口

而上报地址为
```yaml
http://localhost:8080
```
### 以llob为例
#### 使用ws适配器
![img.png](核心功能/img/llob2.png)
#### 使用http适配器
![img.png](核心功能/img/llob.png)
## 适配器
如果你都是默认的配置，就不用动。改了的话，这里跟着改就完事。
### http适配器
```yaml
adapter:
  access_token: "any_access_token" #onebot实现部分为空则不用改
  http_sever:       #bot的运行端口，onebot的事件上报到这里
    host: "0.0.0.0"
    port: 8080
  http_client:
    url: "http://127.0.0.1:3000" 
```
### ws适配器
```yaml
adapter:
  access_token: "any_access_token" #onebot实现部分为空则不用改
  ws_client:
    ws_link: "ws://127.0.0.1:3001"
```