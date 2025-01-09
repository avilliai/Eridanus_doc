---
sidebar_position: 1
---
# 部署
写在前面：
Eridanus和Manyana一样，使用了大量的yaml文件以为用户提供充分的自定义空间。

但目前的Eridanus并未制作启动器兼yaml编辑器，为避免您因不熟悉yaml语法而遇到困难，我们制作了一些教程以帮助您更好地使用此项目。
- [lesson1 基本yaml语法](https://eridanus-doc.netlify.app/docs/lessons/lesson1) 

## 1.onebot实现与适配器配置
需要开启onebot实现的正向websocket服务。
### 安装llob或napcat
- [napcat](https://napneko.github.io/) 优势：低占用，一键包启动方便。
  - 需要手动开启websocketsever服务(见napcat文档)，端口为默认3001,accessToken留空不要填。
- [llob](https://llonebot.github.io/zh-CN/guide/getting-started) 优势：适合铸币
  - 全部保持默认配置即可

完成部署后启动
## 2.部署Eridanus(二选一)
Eridanus不像Manyana为“小白”准备了默认免费对话模型，对话等功能需要参照后续文档自行配置。
### 用部署工具搭建
[下载整合包，教程也在里面](https://github.com/avilliai/Eridanus/releases)
### 不用部署工具搭建(不推荐)
#### 克隆仓库 
确保你已经安装了【git】，找一个你喜欢的目录，在该文件夹打开cmd。

从以下几条指令选一条输入
```yaml
git clone --depth 1 https://github.com/avilliai/Eridanus.git
或使用镜像源
git clone --depth 1 https://mirror.ghproxy.com/https://github.com/avilliai/Eridanus.git
其他镜像源(推荐)
git clone --depth 1 https://github.moeyy.xyz/https://github.com/avilliai/Eridanus.git
```
#### python环境
[下载python3.11](https://mirrors.huaweicloud.com/python/3.11.0/python-3.11.0-amd64.exe)

双击开始安装，第一步【一定要勾选add to path】
#### 修改配置文件
如果你需要修改bot名称，这部分在`Eridanus/config/basic_config.yaml`

bot和master之外的配置项不建议动，除非你知道自己在做什么。
#### 安装依赖与启动
双击Eridanus/一键部署脚本.bat

等待安装完成，双击 启动脚本.bat




