---
sidebar_position: 7
---
# JMComic/asmr/iwara
## jmcomic功能
**此功能需要配置`api.yaml.proxy.http_proxy`**。
### 验车
```yaml
验车1046487
```
### 下载
```yaml
JM下载1046487
```
### 随机本子
```yaml
随机本子
```
### 搜索
```yaml
jm搜{关键字}
```
### 函数调用
```yaml
直接告诉bot你要验车或者下载，或者搜索就可以了。
```
## asmr功能
需要安装ffmepg，并配置好环境变量。

预计之后会将ffmepg的一键安装包并入Eridanus整合包。

此功能需要配置卡片签名，卡片签名地址：https://ss.xingzhige.com/music_card/card

napcat和llob都有配置卡片签名的地方，自己找。
### 指令
```yaml
随机奥术
随机asmr
最新asmr
热门asmr
```
### 配置
`config/settings.yaml`
```yaml
asmr:
  with_url: false  #是否附带原始音频url
  with_file: false #是否合并并发送音频文件
```
默认关闭，开启后上传文件速度与服务器带宽有关，建议关闭。

`config/controller.yaml`
```yaml
resource_search:   #资源搜索功能
  asmr:
    asmr_level: 0  #设置权限。
```
### 函数调用
```yaml
帮我下载https://asmr.one/work/RJ01275524
```
## iwara功能
```yaml
iwara搜{关键字}   #比如 iwara搜菲比
iwara下载{视频id}  #比如 iwara下载ciGDn8TIwYvfgR
iwara最新
iwara热门
iwara趋势
```