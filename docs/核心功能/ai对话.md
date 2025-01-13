---
sidebar_position: 1
---
# ai对话
## 触发方式

群聊内：`@bot 你好` 

私聊：`你好`
## 配置文件
文件来源 config/api.yaml
```yaml
#这里的可能和正式文件有差异，但关键配置项会在这里讲明白，这些不会改变。
llm:
  model: gemini #选择使用的模型(这里是大类别，具体模型在底下填)，用什么配什么
  #模型大类可选openai gemini两种。剩下自己在下面配置。
  system: "你现在是一只猫娘，你的名字是vilm，我的名字是{用户}，是你的主人。"
  func_calling: True #是否开启函数调用功能
  prefix:
      - "."
      - "。"
      - "叮咚鸡"
  enable_proxy: False
  max_history_length: 100 #最大聊天记录条数
  Quote: False #回复时是否引用
  focus_time: 60  #单次触发对话后持续有效时间
  openai:
    api_keys:
      - YOUR_API_KEY_1
      - YOUR_API_KEY_2
    model: glm-4-flash
    quest_url: https://open.bigmodel.cn/api/paas/v4/chat/completions #完整调用地址。只填base_url不行
  gemini:
    api_keys:
      - YOUR_API_KEY_1
      - YOUR_API_KEY_2
    model: gemini-2.0-flash-exp
    base_url: https://generativelanguage.googleapis.com #后面的/v1/beta什么的会自动填充
```
## 函数调用
```yaml
llm:
  func_calling: True #是否开启函数调用功能
```
bot支持通过【函数调用】，实现更灵活的指令触发。
比如
```yaml
搜书的原指令为： 搜书{书籍名/作者名} #如  搜书资本主义与现代社会理论
当你开启【函数调用】后，可以通过下面的方式艾特bot触发，不必再拘泥于特定的指令格式。
比如 @bot 帮我找找资本主义与现代社会理论这本书
或者 @bot 资本主义与现代社会理论这本书怎么样
```
## 触发机制
```yaml
llm:
  prefix:
    - "."
    - "。"
    - "yucca"
  focus_time: 60  #单次触发对话后持续有效时间
```
这两项允许你，
- 以` . 或 。 或 yucca `作为前缀触发ai对话而无需艾特，你可以继续像这样增加匹配的前缀。
- 在一次触发对话后，60s内无需艾特，持续对话持续刷新时间。
## 清理对话
```yaml
/clear
如开启函数调用，可直接告诉bot【清理当前对话】
master也可使用【清理所有人的对话记录】之类的话来清理所有人的对话记录。
```
## 申请apikey
### gemini配置方式
#### 1、获取gemini apikey
[先获取Gemini apikey](https://ai.google.dev/tutorials/setup?hl=zh-cn) (获取过程需要开启代理，打不开/地区不可用就是你机场不行。)

打开config/api.yaml
```yaml
#这里省略了其他配置项，不代表你可以随便删除其他配置项。
llm:
  model: gemini #选择使用的模型大类。
  system: "你现在是一只猫娘，你的名字是{bot_name}，我的名字是{用户}，是你的主人。"
  enable_proxy: False
  gemini:         #https://ai.google.dev/
    api_keys:
      - YOUR_API_KEY_1   #这里填入你的apikey，有几个填几个，多key填写示例如下。
      - YOUR_API_KEY_2
    model: gemini-2.0-flash-exp
    base_url: https://generativelanguage.googleapis.com #后面的/v1/beta什么的会自动填充
```
#### 2、配置正向代理/反向代理(二选一)
只配置apikey，但不配置proxy是不行的。
##### 反向代理
反向代理配置难度较低，建议使用。
```yaml
一些你可以使用的反代地址，不保证全都能用。
https://dainty-liger-d8726e.netlify.app
https://calm-taiyaki-bb86b0.netlify.app
https://inspiring-piroshki-716f76.netlify.app
https://fbsvilli.netlify.app
https://mellifluous-cupcake-ea08ad.netlify.app
https://fsadfafsfdsafsa.netlify.app
https://voluble-frangipane-db8db1.netlify.app

如果你想要搭建自己的反向代理，自行查看https://simonmy.com/posts/%E4%BD%BF%E7%94%A8netlify%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86google-palm-api.html。
```
```yaml
#省略了其他配置项，不代表你可以随便删除其他配置项。
llm:
  model: gemini 
  system: "你现在是一只猫娘，你的名字是{bot_name}，我的名字是{用户}，是你的主人。"
  enable_proxy: False
  gemini:    
    base_url: https://mellifluous-cupcake-ea08ad.netlify.app  #填写了一个反代地址
```
##### 正向代理
取决于你自己的代理软件，我不能给你一个准确答案。如果你看不懂就老老实实用反代。
```yaml
#省略了其他配置项，不代表你可以随便删除其他配置项。
llm:
  enable_proxy: True 
proxy:
  http_proxy: "http://127.0.0.1:10809"  #本地代理软件的的http代理端口。
```
### open标准模型配置方式
文心、讯飞星火、chatglm、豆包、kimi都可以使用此配置方式

不再赘述。爱折腾这块的多少都知道怎么做。
#### 代理
```yaml
llm:
  enable_proxy: False
```
部分模型的使用，需要配置代理。当你配置了proxy中的http_proxy后，启用此项，bot将自动使用你配置的代理。