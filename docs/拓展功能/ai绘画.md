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
## kaggle部署ai绘画(必看)
下面的教程将带你实现白嫖kaggle的gpu资源。

【inspired by [spawner](https://www.kaggle.com/spawnerqwq)】
### kaggle注册登录
[kaggle](https://www.kaggle.com/code/spawnerqwq/qqbot-simple-reforge-spawner)

记得**绑定手机号**，不然用不了gpu和联网。

`在哪绑？我忘了，自己找去。`
### cpolar注册
去[cpolar](https://dashboard.cpolar.com/get-started)注册(选免费套餐)，然后点验证，复制你的隧道 Authtoken

记录你的cpolar密钥 即隧道AuthToken，比如`YTMgojjgnagtnbvjppf`(这是我乱打的，你并不能偷懒直接拿去用)
### kaggle脚本修改
打开[spawner的脚本](https://www.kaggle.com/code/spawnerqwq/qqbot-simple-reforge-spawner)，点击白色的copy&edit，跳转到新页面后往下划拉。

![img.png](./img/kaggle.png)
把图中的`cpolar密钥`换成你上面申请的隧道AuthToken，看起来应该是这样
```python
cpolar_use = True
if cpolar_use:
    !curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash
    !cpolar version
    !cpolar authtoken YTMgojjgnagtnbvjppf
    def iframe_thread_1():
        !cpolar http 7860    #网页
    t1=threading.Thread(target=iframe_thread_1)
    t1.start()
    !wget -q -O - ipv4.icanhazip.com
    author = 'spawner'
```
### 设为公开脚本
点击页面右上角的share，将脚本设置为公开，这是为了其他账号能够正常访问。
![img.png](./img/kaggle1.png)
**记录下这里的public url**，然后点击save。
```yaml
https://www.kaggle.com/code/xxxx/qqbot-simple-reforge-spawner
```
这个【分享链接】我们待会会用到。
### 为持久化运行做准备
多注册一些账号，记录好账号密码，同时每一个账号都需要完成手机号验证，否则无法使用。

等下我们会用到。

验证码部分你可以找接码平台。
## 部署Achernar
[Achernar](https://github.com/avilliai/Achernar)

Achernar是Eridanus的派生项目。从[release](https://github.com/avilliai/Achernar/releases)下载最新的发行版。
### 安装chrome浏览器
自己装吧，不教了
### 编辑Achernar配置文件
`Achernar/config.yaml`
```yaml
proxy: ""     #没用，不用管这一项
port: 3529
#在shared_notebook填入上面记录的你的【分享链接】
shared_notebook: "https://www.kaggle.com/code/xxxx/qqbot-simple-reforge-spawner"           
enable_kaggle_extension: true
enable_cpolar_extension: true
cpolar_check_interval: 3600        
kaggle_change_account_interval: 36000   

kaggle_accounts:
  - email: "你的kaggle账号"
    password: "密码"
  - email: "你的第二个kaggle账号"
    password: "密码"  #以此类推
cpolar:
  email: "你的cpolar账号"
  password: "密码"
```
**运行Achernar.exe**
### 配置Eridanus
`config/api.yaml`
```yaml
ai绘画:
  sdUrl: "http://127.0.0.1:3529" 
  sd审核和反推api: "http://127.0.0.1:3529"
  nai_key: ""
```
重启Eridanus以重载配置文件。 至此，你应该已经可以在群里使用
```yaml
画 xxx #
```
