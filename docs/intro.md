---
sidebar_position: 1
---
# 部署
后续会发布专门的部署工具

## 1.onebot实现与适配器配置
**请配置【ws适配器】。**

使用ws适配器时，需要开启onebot实现的正向websocket服务。

### 安装llob或napcat
- [napcat](https://napneko.github.io/) 优势：低占用，一键包启动方便。
  - 需要手动开启websocketsever服务(见napcat文档)，端口为默认3001,accessToken留空不要填。
- [llob](https://llonebot.github.io/zh-CN/guide/getting-started) 优势：适合铸币
  - 全部保持默认配置即可

完成部署后启动
## 2.部署Eridanus
以下三选一。

Eridanus不像Manyana为“小白”准备了默认免费对话模型，对话等功能需要参照后续文档进行配置。
### 用部署工具搭建
`没做呢`
### 从Manyana到Eridanus
[下载 FMTE.rar 并解压](https://github.com/avilliai/Eridanus/releases/tag/FMTE)。
### 不用部署工具搭建
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
### 安装依赖与启动
双击Eridanus/一键部署脚本.bat

等待安装完成，双击 启动脚本.bat




