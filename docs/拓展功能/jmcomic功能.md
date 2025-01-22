---
sidebar_position: 7
---
# JMComic&asmr功能
## jmcomic功能
**此功能需要配置proxy**。
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
## asmr功能
需要安装ffmepg，并配置好环境变量。

预计之后会将ffmepg的一键安装包并入Eridanus整合包。
### 指令
```yaml
随机奥术
随机asmr
```
该功能支持函数调用，你可以直接告诉bot你想听asmr。
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