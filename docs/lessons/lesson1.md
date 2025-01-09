---
sidebar_position: 1
---
# Lesson 1: 基本yaml语法
大部分用户并没有耐心去[runoob.com](https://www.runoob.com/w3cnote/yaml-intro.html) 学习yaml语法，而实际上，就使用Eridanus所需要的yaml语法掌握程度而言，通过耗费几分钟阅读本节，您将避免很多不必要的麻烦。

## 关于 "-"
```yaml
gemini:
	- xxxxxx
	- xxxxxx
```
”-“ 在这里的意思是，告诉读取yaml的bot：对应的值是列表的一部分。什么是列表？你可以把它想象为一列火车，有着许多火车车厢，而bot使用时则是从中选择一节“车厢”；即使只有一节车厢，火车也仍然是火车，这一规则必须得到遵守。

**`-`的后面需要有一个空格，变成`- 具体的填写内容`才能生效**
```
gemini: 
  api_keys: 你的key     #这是一个错误填写示例，因为你删去了- 。bot的逻辑是，从【火车】中选取一节【车厢】，当你直接把【车厢】暴露在bot面前，bot将无法处理，因为对bot而言，读取到的数据不再是【火车】。
-------------正确示例如下-------------------
gemini:         #https://ai.google.dev/
  api_keys:
    - YOUR_API_KEY_1
    - YOUR_API_KEY_2
------------------------------------
gemini:
  api_keys:
	- xxxxxx      #这样写也可以
-------------错误示例如下-------------------
gemini:
  api_keys:
- xxxxxx      #这样的问题在于破坏了yaml文件本身的结构，对bot来说，是要先找到【gemini】再找【api_keys】，最后从【api_keys】中选取一节【车厢】，这是一个严格的逻辑流程，缩进错误不仅破坏了这一逻辑流程，也不符合yaml语法。
```
为什么要用多key?或者说，为什么要用【火车】拉【车厢】？

与增加车厢提高载客量一样，我们不使用`api_keys: key`是因为，考虑到部分bot面向的用户量比较大，因此使用列表(车厢)能够通过填写多个apikey以分散单个apikey的压力。(google会有每分钟请求限制)

你可以看到，我们在使用openai sdk的时候也使用了同样的思路。
# 关于 ":"
在yaml文件中`：`无法被读取，而`:`可以，并且`:`后面需要加一个空格变成`: `，这样才是一个完整的yaml键值对`key: value`
# 关于"True"和"true"
在yaml文件中，这两种写法都能被读取为boolean值，所以两种写法都可以，`false`和`False`也是同理。
# 关于数字
在python中，能转为int类型的数据，在yaml文件被读取时都会被转为int。
# 关于`key: value`以及嵌套结构(拓展)
**请注意，既定的项目的yaml文件结构中每一对key: value均有其特定用处，如果您不是开发者，不要随意变动yaml文件结构，否则可能导致项目运行异常或功能缺失。**

你可能需要回顾一下数据类型的知识了。

key可以对应多种数据类型，比如我们上面的
```yaml
key: value
key2:
- value1
- value2
- value3
key3:
	sonKey: 
	- songvalue1
	- songvalue2
	- songvalue3
	- {grandsonkey: songvalue4}
	sonKey2:
		grandsonkey: grandsonValue
		grandsonkey1: grandsonValue1         #它可以无限嵌套下去
		grandsonkey12: 
			grandgrandsonkey1: grandgrandsonValue1 
			grandgrandsonkey2:
			- grandgrandsonValue1 
			- grandgrandsonValue2
			- grandgrandsonValue3
```
嵌套结构在yaml文件中很常见，在Manyana和Eridanus中也得到了较为广泛的使用。
