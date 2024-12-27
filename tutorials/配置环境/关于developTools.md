---
sidebar_position: 2
---
# sdk
如前所述
【Eridanus项目】和【Eridanus sdk】不是一个东西。
- 【Eridanus项目】即主仓库，已经完成了诸多功能。
- 【Eridanus sdk】是为其他开发者提供的开发工具，使你能够另起炉灶编写bot源码

在实际应用中，如果你是从零开始构建bot，那么你该使用的就是Eridanus sdk

如果你是继续在【Eridanus项目】基础上开发，那么你该使用的就是developTools
## Eridanus自带的developTools
你应该可以看到，项目根目录有一个developTools文件夹，它就是我们开发要使用的工具。

该sdk修改自[yiriob](https://github.com/YiriMiraiProject/YiriOneBot)

你可以用它实现收发等一系列任务，详情请查看【关于sdk】。

接下来，教程将带你完成第一个消息收发任务。
## pypi版本
**暂未发布**，发布后你可以使用
`pip install Eridanus`
来安装该sdk
## 开始吧