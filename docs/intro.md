---
sidebar_position: 1
---
# 部署
如果您是使用【Eridanus sdk】的开发者，请移步【教程】。
## 快捷部署
[linux脚本](https://gitee.com/laixi_lingdun/eridanus_deploy)

[windows整合包](https://github.com/avilliai/Eridanus/releases)

如使用快捷部署部署失败，请参照文档剩余部分部署。
## 一般部署流程
### 1.onebot实现与适配器配置
需要开启onebot实现的正向websocket服务。
#### 安装llob或napcat
- [napcat](https://napneko.github.io/) 优势：低占用，一键包启动方便。
  - 需要手动开启websocketsever服务(见napcat文档)，端口为默认3001,accessToken留空不要填。
- [llob](https://llonebot.github.io/zh-CN/guide/getting-started) 优势：适合铸币
  - 全部保持默认配置即可

完成部署后启动
### 2.部署Eridanus
【快捷部署】应当完全能够帮你完成接下来的步骤，但以防万一，这里将介绍不使用【快捷部署】时的搭建方式。
#### 克隆仓库 
确保你已经安装了【git】，找一个你喜欢的目录，在该文件夹打开cmd。从以下几条指令选一条输入
```yaml
git clone --depth 1 https://github.com/avilliai/Eridanus.git
或使用镜像源
git clone --depth 1 https://mirror.ghproxy.com/https://github.com/avilliai/Eridanus.git
其他镜像源(推荐)
git clone --depth 1 https://github.moeyy.xyz/https://github.com/avilliai/Eridanus.git

git clone --depth 1 https://ghfast.top/https://github.com/avilliai/Eridanus.git

git clone --depth 1 https://gh.llkk.cc/https://github.com/avilliai/Eridanus.git
```
#### python环境
[下载python3.11](https://mirrors.huaweicloud.com/python/3.11.0/python-3.11.0-amd64.exe)

双击开始安装，第一步【一定要勾选add to path】
#### 修改配置文件
如果你需要修改bot名称，这部分在`Eridanus/config/basic_config.yaml`。bot和master之外的配置项不建议动，除非你知道自己在做什么。

其他配置文件按需修改。
#### 安装依赖与启动
双击Eridanus/一键部署脚本.bat

等待安装完成，双击 启动脚本.bat




