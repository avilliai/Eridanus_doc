---
sidebar_position: 5
---
# ai绘画
## 接入你自己的sd
配置文件`config/api.yaml`
```yaml
ai绘画:
  sdUrl: '' #你自己搭建的sd，地址，示例http://127.0.0.1:17858（示例≠你能直接填示例用），部署https://www.bilibili.com/video/BV1iM4y1y7oA/
  sd审核和反推api: ''        # 如果你的sd有反推插件https://github.com/spawner1145/stable-diffusion-webui-wd14-tagger.git，可以直接使用你的sdurl的api
  nai_key: ''
```
## 指令
### novel_ai绘图指令
```yaml
n4 prompt  #比如 n4 an anime girlish
n3 prompt  #比如 n3 an anime girlish
```
### sd绘图指令
```yaml
画 xxxxx
```
### tag反推
```yaml
tag
```
然后发送图片
### 重绘
```yaml
重绘
```
然后发送图片
### 指令设置参数
```yaml
setsd xxxx   #设置sd参数
setre xxxx   #设置重绘参数
```
### 模型查询指令
```yaml
lora
ckpt 
```
### 切换模型
```yaml
ckpt2 {modelname}
```
