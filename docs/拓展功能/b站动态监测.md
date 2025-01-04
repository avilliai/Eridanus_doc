---
sidebar_position: 8
---
# b站动态监测
## 指令
```yaml
/bili add {uid}  #不用带{}  
/bili remove {uid}  #不用带{}  
```
分别对应添加和删除任务。

直播检测以后做
## 配置方式
更新脚本-3 playwright工具安装
![image.png](./img/playwright.png)

### 进阶——函数调用
b站订阅查询支持函数调用，当config/api.yaml配置了对话模型并启用了函数调用
```yaml
llm:
  func_calling: True #是否开启函数调用功能
```
你可以不遵循特定指令格式
```yaml
@bot 订阅b站的1556651916
```