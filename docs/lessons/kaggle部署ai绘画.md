![QQ20250410-220311](https://github.com/user-attachments/assets/f82e603c-862a-4c1f-9ceb-0f8afcf70c59)---
sidebar_position: 1
---
# kaggle部署ai绘画服务
kaggle每周有30h免费gpu时长，每个脚本一次可以运行12h，所以当你有7个号的时候，就可以无限续杯了。

[kaggle注册](https://www.kaggle.com/code/spawnerqwq/qqbot-simple-reforge-spawner)，记得`在profile界面`  **绑定手机号**，不然用不了gpu和联网。
## kaggle脚本修改
**脚本二选一**

**frp和cpolar二选一**

[双卡脚本](https://www.kaggle.com/code/spawnerqwq/qqbot-simple-reforge-spawner) 建议使用。

[旧版脚本](https://www.kaggle.com/code/lzrea06/qqbot-simple-reforge-spawner-bfef6d) 旧版脚本
### 使用frp
免费frp有很多，以[chml](https://panel.chmlfrp.cn/tunnelm/manage)为例。在其官网注册登录，并完成实名验证(怕个人信息泄漏的换别的frp服务也行，流程基本一样)。
![fc8578c69e33882d300b258902051516.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/fc8578c69e33882d300b258902051516.png)
![image.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/20250126101517.png)

![image.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/20250126101914.png)

好的，你现在得到了frp配置文件，它看起来如上图(图炸了挂梯子刷新)，让我们回到kaggle。

打开【脚本】后，点击白色的copy&edit，跳转到新页面后你可以看到：  
![image.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/20250126102141.png)
用你刚刚复制的配置文件内容替换掉这一坨。双卡脚本需要把配置文件拆成两份粘贴。

让我们回到chml，**在【隧道列表】记录【连接地址】**
![image.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/20250126102449.png)
你得到了类似下面这样的连接地址
```yaml
hb.fuck.you:114514 
```
那我们就**记录**下面的内容。
```yaml
http://hb.fuck.you:114514  #加上了http://
```
### 使用cpolar
去[cpolar](https://dashboard.cpolar.com/get-started)注册(选免费套餐)，然后点验证，复制你的隧道 Authtoken ，比如`YTMgojjgnagtnbvjppf`(这是我乱打的，你并不能偷懒直接拿去用)

打开【脚本】后，点击白色的copy&edit，跳转到新页面后往下找到：
![kaggle.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/kaggle.png)

把图中的`cpolar密钥`换成你上面申请的隧道AuthToken，看起来应该是这样
```python  
cpolar_use = False
if cpolar_use:
    !curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash
    !cpolar version
    !cpolar authtoken Y2IyNsdfafsaFUIHGGUAHOFMxYmE0
    def iframe_thread_1():
        !cpolar http 7860    #网页
    t1=threading.Thread(target=iframe_thread_1)
    t1.start()
    !wget -q -O - ipv4.icanhazip.com
    author = 'spawner'
```  
## 设为公开脚本
点击页面右上角的share，将脚本设置为公开，这是为了其他账号能够正常访问。  
![kaggle1.png](https://raw.githubusercontent.com/avilliai/imgBed/master/images/kaggle1.png)

**记录下这里的public url**，然后点击save。
```yaml  
https://www.kaggle.com/code/xxxx/qqbot-simple-reforge-spawner  
```  
这个【分享链接】我们待会会用到。
## 更多备用账号
注册更多账号，记录好账号密码。**你注册的所有账号都需要能够通过 email+密码 登录，并且完成了手机号验证**

验证码部分你可以找[接码平台](https://sms-activate.guru/en/email-activations)。

**这些账号注册后，只要完成手机号验证就可以，不用别的操作。** 但要注意，不要出现同一台设备同时登陆了两个kaggle账号的情况，可能会被封，换号时注意退出登录。
## 部署Achernar
[Achernar](https://github.com/avilliai/Achernar)

### 拉取项目源码
```
git clone https://github.com/avilliai/Achernar
或使用镜像源  
git clone --depth 1 https://mirror.ghproxy.com/https://github.com/avilliai/Achernar
其他镜像源(推荐)  
git clone --depth 1 https://github.moeyy.xyz/https://github.com/avilliai/Achernar
```
不会用git自己看[avilliai/Achernar: kaggle账号自动切换+运行项目/cpolar隧道本地反向代理](https://github.com/avilliai/Achernar)页面右上角有个绿色按钮，点了下载zip压缩包。
### 安装python
[安装python3.11](https://mirrors.huaweicloud.com/python/3.11.0/python-3.11.0-amd64.exe)

记住第一步勾选add to path，剩下全默认。
### 安装依赖
运行`一键部署脚本.bat`

### 编辑Achernar配置文件
`Achernar/config.yaml`
```yaml
proxy: ""     #frp不用管。登录kaggle时使用的代理。  
quest_proxy: ""  #frp不用管。sd api请求时使用的代理地址，如果开启代理后，Achernar反代不能正常工作请填写此项。你代理软件的http代理地址。取决于具体情况，clash一般http://127.0.0.1:7890  
port: 3529       
headless: true   
#在shared_notebook填入你记录的【分享链接】  
shared_notebook: ""  
enable_kaggle_extension: true  
enable_cpolar_extension: true    #使用frp就将这个改成false
cpolar_check_interval: 180  
kaggle_change_account_interval: 39600  
  
kaggle_accounts:  
  - email: "你的邮箱"  
    password: "你的密码"  
  - email: "你的第二个邮箱"  
    password: "你的第二个密码"  #以此类推  
cpolar:                  #使用frp不用填
  email: "cpolar的邮箱"  
  password: "cpolar的密码"  
  
  
```  
**运行Achernar主程序**，有条件的话，建议开启代理，并设置为pac模式/规则代理模式，将有助于稳定运行。
```yaml
此时部署完成，如果你是开发者可以自行对接，其他使用sd api的项目也可以接入。

如果你使用cpolar，就以http://127.0.0.1:3529作为base_url，发送绘图请求。

如果你使用frp，以在frp配置步骤记录的【连接地址】(加上http://)作为base_url，发送绘图请求。

url=f'{base_url}/sdapi/v1/txt2img'
```

## 配置Eridanus
### 如使用frp
`config/api.yaml`
```yaml  
ai绘画:  
  sdUrl:    
  - "http://hb.fuck.you:114514"  #在frp配置步骤记录的【连接地址】(加上http://)
  sd审核和反推api: "http://hb.fuck.you:114514"   #和上面的一样
  nai_key: ""  
```  
### 如使用cpolar
`config/api.yaml`
```yaml  
ai绘画:  
  sdUrl:    
  - "http://127.0.0.1:3529"  #Achernar，反代地址。你可以继续增加其他服务端地址。  
  sd审核和反推api: "http://127.0.0.1:3529"  
  nai_key: ""  
```  
### 配置settings
`config/settings.yaml`
```yaml  
ai绘画:  
  sd画图: true  
  sd默认启动模型: 'noobaiXLNAIXL_vPred10Version.safetensors'  #底模。你可以改成miaomiao_1_4.safetensors。  
  sd图片是否保存到生图端: false   #是否将生成的图片保存在webui的outputs里  
  novel_ai画图: false  
  no_nsfw_groups:               #禁止色图的群号  
  - 111  
  - 222
  - 333  
```  
重启Eridanus以重载配置文件。   
至此，在Achernar自动运行的kaggle脚本完全启动后(大概需要十分钟)，你就可以使用对应的指令了。
```yaml  
画 xxx #根据指定prompt生成图片  
tag    #反推图片prompt  
重绘 xxxx
```

Achernar的原型脚本和kaggle脚本均来自[spawner](https://github.com/spawner1145)

## 如果不想部署Achernar
- 找到右上角的save versions并点击
![QQ20250410-220212](https://github.com/user-attachments/assets/bc46ccf6-7d01-48c6-88ba-dc8e4515e686)
- 按照图里的设置选择并点击save
![QQ20250410-220243](https://github.com/user-attachments/assets/8ab24516-7d03-4e32-87b8-d36c7cb9be6e)
- 可以发现左下角出现了黄色标记，这代表着代码开始运行了
![QQ20250410-220311](https://github.com/user-attachments/assets/1e29546e-aace-4ad3-adee-8e897d7fd6b9)
- 点击那个地方，再点击出来的三个小圆点，你可以看到`open logs in viewer`的选项，点击它可以进入控制台查看代码当前运行的状态
![QQ20250410-220318](https://github.com/user-attachments/assets/7c0927ae-b5f6-4b73-9028-0b7d4b36dd2c)
- 当你看到`running on local url`这样的字眼时，说明webui已经启动，这个时候如果你开了内网穿透，就可以使用ai画图了
![QQ20250410-220441](https://github.com/user-attachments/assets/e12e648f-1e45-493b-99f7-c088a65524f2)
