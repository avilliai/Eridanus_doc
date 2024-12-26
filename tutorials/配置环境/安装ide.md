---
sidebar_position: 1
---
# 安装ide

如果你是使用部署工具搭建的，那么你应该已经有了Eridanus文件夹，用你的ide打开它，将python解释器选定为项目附带的python。省去再度配置环境的麻烦

如果你还没有获取源码，自行fork仓库，这样能够使你参与到项目的开发中。

接下来的教程假设`你既不懂git怎么用，也不知道怎么配置python环境，`
## 安装ide
二选一

[pycharm社区版](https://blog.csdn.net/wangmeixi/article/details/103840541)

[vsc](https://blog.csdn.net/leah126/article/details/131661331)
## 安装git
[git安装教程](https://blog.csdn.net/mukes/article/details/115693833)

其实开始安装后无脑下一步就行。
### 克隆仓库
```yaml
#找一个你喜欢的目录，打开cmd，下面指令任选其一
git clone --depth 1 https://github.com/avilliai/Eridanus.git
或使用镜像源
git clone --depth 1 https://mirror.ghproxy.com/https://github.com/avilliai/Eridanus
其他镜像源(推荐)
git clone --depth 1 https://github.moeyy.xyz/https://github.com/avilliai/Eridanus
```
你将得到Eridanus文件夹。

使用你的ide，打开Eridanus文件夹。
## 安装python3.11
[安装python3.11](https://blog.csdn.net/MichaelJiangJunC/article/details/129996726)
## 在ide中配置python解释器
### 配置解释器
[懒得教](https://blog.csdn.net/qq_42432673/article/details/108440370)

选刚才安装的python3.11。

**如果你用的搭建工具获取的Eridanus**，environments里面有一个python3.11/python.exe了，解释器直接选它，既不用再【装python3.11】也不用【安装依赖】
### 安装依赖
pycharm或者vsc都有一个terminal或者叫终端，点开它。输入下面的指令
```yaml
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip install -r requirements.txt
```
好了，你配置完环境了，准备开发去吧。