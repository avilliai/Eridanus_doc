---
sidebar_position: 2
---
# 消息链
## 从原始数据到消息链
### 原始数据
在onebot实现上报给你的消息中，原始数据可能是这样的。
```
{
'self_id': 1000000,
'user_id': 111111111,
'time': 114514,
'message_id': 1253451396,
'real_id': 1253451396,
'message_seq': 1253451396,
'message_type': 'group',
'sender':
    {'user_id': 111111111, 
      'nickname': '主人', 
      'card': '', 
      'role': 'member', 
      'title': ''},
'raw_message': "(乱七八糟的CQ码我就不写了，不建议使用raw_message)",
'font': 14,
'sub_type': 'normal',
'message': [
  {
    'type': 'text', 
    'data': 
    {'text': '这里是测试文本'}
  }, 
  {
    'type': 'image', 
    'data': 
    {
      'file': 'DE391381BB704007BBA4F80CD05E4D6B.jpg', 
      'subType': 0, 
      'url': 'https://multimedia.nt.qq.com.cn/download?appid=1407&fileid=EhT45MAp_s2okuaeSpTznxugUwSnJBjIqDYg_woozpavsqDPiwMyBHByb2RQgL2jAVoQAxg63F0dTfY4ZGBgImYCmw&spec=0&rkey=CAISKKSBekjVG1fM9OVJfwjzD6VKXt5niqfyzymF5Y0RGWh5X1AB_EyLgtk', 
      'file_size': '889928'
    }}],
'message_format': 'array',
'post_type': 'message',
'group_id': 879886836
}
```
对我们而言，除了发送者信息(id、所在群、昵称等)外，最重要的就是message字段的内容了。

但是，如果想要从原始数据中拿到这些内容，我们就不得不不厌其烦地对json进行解析，这实在过于麻烦。

所以，我们需要一个更高效的办法来处理原始数据，这就是消息链。
### 消息链
【消息组件】即一条消息的构成，你在群内发送的"你好[图片]"，实际上是由两个消息组件构成的：
```yaml
[
  {"type": "text", "data": {"text": "你好"}}
  {"type": "image", "data": {"file": "xxx.jpg", "url": "https://xxx.jpg", "file_size": "12345"}}
]
```
解析它实在令人头大，为了更方便地构建消息组件和解析消息组件，我们引入了 消息链（MessageChain）的概念。。

**消息链会将消息列表分解为多个消息组件对象，使你能够更加方便地处理消息内容。**

消息链的结构如下：
```yaml
[Text(comp_type='text', text='呷玛日巴今天的运势是：'), 
Image(comp_type='image', file='file://D:/python/Eridanus/DF3851D38B81705C040377464385D3F5.jpg', url='https://multimedia.nt.qq.com.cn/download?appid=1407&fileid=EhQm6tFO_dvhCm7uGARda2ccMEu7zBienS4g_woowfajr8fPiwMyBHByb2RQgL2jAVoQMssHxFAPRYs3PCDsQfgsxg&spec=0&rkey=CAISKKSBekjVG1fMrpFoAHgCdk_rDNx6mxVmATYCwsRJAXzZEhK2xjkUl_M', type='')
]
```
消息组件变成了相应的对象，你可以通过属性和方法来获取消息组件的具体信息。
```python
@bot.on(GroupMessageEvent)
async def handle_group_message(event: GroupMessageEvent):
    print(event.message_chain)
    if event.message_chain.has(Image):
        print(event.message_chain.get(Image)[0].url)
    if event.message_chain.has(Text):
        print(event.message_chain.get(Text)[0].text)
```
其他属性同样可以获取，具体有什么属性可用见下一章节【消息组件】
## MessageChain可用函数
### 纯文本
```yaml
替代原来的raw_message，返回纯文本消息内容
等价于event.message_chain.get(Text)[0].text，如果消息链除了Text还有其他元素，就会返回""
```
### 判含
```yaml
event.message_chain.has(comp_type)
```
判断是否包含某种消息组件
### 取
```yaml
event.message_chain.get(comp_type)
```
提取消息链中所有指定元素，整合为列表(如果消息链中包含执行元素的话)