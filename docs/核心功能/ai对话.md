---
sidebar_position: 1
---
# ai对话
## 触发方式

群聊内：`@bot 你好`

私聊：`你好`
## 配置方式
config/api.yaml
```yaml
llm:
  model: gemini        #选择使用的模型(这里是大类别，具体模型在底下填)，用什么配什么
  system: "你现在是一只猫娘，我的名字是{用户}，是你的主人。"
  prefix: "."                #通过指定前缀触发
  enable_proxy: True
  max_history_length: 100    #最大聊天记录条数
  Quote: False               #回复时是否引用
  focus_time: 60             #单次触发对话后持续有效时间
  openai:
    api_keys:
    - 第一个key
    - 第二个key
    model: 模型名
    quest_url: 请求地址 #比如：https://open.bigmodel.cn/api/paas/v4/chat/completions 需要完整调用地址。只填base_url不行
  gemini:
    api_keys:
      - 第一个key
      - 第二个key
    model: gemini-2.0-flash-exp
    base_url: https://generativelanguage.googleapis.com #后面的/v1/beta什么的会自动填充，所以这里可以填项目提供的中转
```
### gemini配置方式


### open-standard-support model 配置方式
文心、讯飞星火、chatglm、豆包、kimi都可以使用此配置方式