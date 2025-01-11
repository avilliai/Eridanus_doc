---
sidebar_position: 2
---
# 接入外部api
## api是啥
api（Application Programming Interface）指应用程序编程接口，你可以通过调用由其他人提供的api服务实现特定功能，而无需编写具体功能的业务实现逻辑。

打个比方，你是顾客，api是服务员，只要你把要吃的菜告诉服务员，然后等待服务员把菜呈上来就行了，而无需其他操作。

接下来我们将以 随机柴郡表情包 为例，展示如何调用外部api
## 定义一个函数
### 选择接口
在api站点找到你想用的接口

[随机柴郡表情包api](https://api.yujn.cn/?action=interface&id=196)

观察得知，这个api的地址为`http://api.yujn.cn/api/chaijun.php` ，同时，它是直接返回图片的，不用传递其他参数。
### 定义函数
我们现在知道，只要向`http://api.yujn.cn/api/chaijun.php` 发送get请求，就可以获取到一张柴郡表情包的二进制数据，所以我们可以这样写。

新建一个python文件，写入下面的内容(假定这里创建的文件名叫做`chaijun.py`)
```python
import httpx
async def chaijun():                              #async def是固定前缀，不能变
    url = "http://api.yujn.cn/api/chaijun.php?"   #柴郡图片的api地址
    async with httpx.AsyncClient() as client:      #使用httpx库发送get请求
        r = await client.get(url)             
        path="pic.png"                          #图片保存路径
        with open(path, "wb") as f:              #将图片保存到本地
            f.write(r.content)
        return path                             #返回图片路径
if __name__ == '__main__':
    import asyncio                  #调用测试
    asyncio.run(chaijun())
```
好的，我们顺利地写出了第一个功能函数，运行这个函数吧，你应该会得到一张柴郡表情包的图片。
## 调用函数
记得上一节我们创建的主函数main.py吗？现在我们可以通过它使用刚才做的柴郡表情包功能了。
```python

from Eridanus.adapters.websocket_adapter import WebSocketBot
from Eridanus.event.events import GroupMessageEvent
from Eridanus.message.message_components import Image, Text
from chaijun import chaijun

bot = WebSocketBot('ws://127.0.0.1:3001')

@bot.on(GroupMessageEvent)
async def _(event: GroupMessageEvent):
    if event.raw_message=="柴郡":
        bot.logger.info("找一张柴郡表情包!")
        path=await chaijun()
        await bot.send(event,Image(file=path))
        #如果你想图文一起发，可以这样写👇
        #await bot.send(event,[Text("柴郡表情包"),Image(file=path)])

bot.run()
```
这样，当你在群里发送 柴郡 的时候，bot就会下载一张柴郡表情包发给你。

恭喜你完成本章节学习。
## 后记：为什么不是requests?
### 同步和异步
在上面柴郡表情包功能实现中，其实还有另一种写法
```python
import requests
def chaijun():                            
    url = "http://api.yujn.cn/api/chaijun.php?"   #柴郡图片的api地址
    r = requests.get(url)             
    path="pic.png"                          #图片保存路径
    with open(path, "wb") as f:              #将图片保存到本地
        f.write(r.content)
    return path                             #返回图片路径
if __name__ == '__main__':
    chaijun()
```
为什么我们不这样写？这样看起来似乎是更加简单且符合直觉的写法。

这是因为requests库的请求是【同步】的，如果你使用这种写法，当bot在执行chaijun指令时，bot将无法执行任何其他指令，直到 柴郡 任务执行完毕。

在 柴郡 任务中，如果你使用【同步】写法，并不会感觉到明显【阻塞】，这是因为因为图片本身体积很小，同步任务执行的很快以至于看起来似乎没有阻塞，一旦换成其他耗时的请求操作，这样写的弊端就会暴露无遗。

httpx是一个【异步】库，异步编程允许程序在等待I/O操作完成时执行其他任务，从而避免了程序在I/O操作期间的空闲等待，因此不会出现阻塞情况。
### 伪异步
```python
#伪异步示例
import requests
async def chaijun():                            
    url = "http://api.yujn.cn/api/chaijun.php?"   #柴郡图片的api地址
    r = requests.get(url)             
    path="pic.png"                          #图片保存路径
    with open(path, "wb") as f:              #将图片保存到本地
        f.write(r.content)
    return path   
```
尽管函数前加上 async 可以使其成为协程函数，但这并不意味着函数内部的操作会自动变为异步。async 只是标记了函数是异步的，函数内部如果调用的是同步操作（例如 requests.get()），那么这些操作依然会阻塞当前线程。因此，async 本身并不会改变函数执行的同步本质，只有使用支持异步的库（如 httpx）才能实现非阻塞的异步操作。
