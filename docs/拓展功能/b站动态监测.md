---
sidebar_position: 8
---
# bilibili相关功能
## 添加/移除订阅
```yaml
/bili add {uid}  #不用带{}  
/bili remove {uid}  #不用带{}  
```
分别对应添加和删除任务。

直播检测以后做
## 热门
```yaml
今日热门    #后续加入定时任务中。
```
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