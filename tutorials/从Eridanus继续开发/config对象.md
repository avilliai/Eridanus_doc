---
sidebar_position: 3
---
# config对象
YAMLManager是【Eridanus项目】中提供的类，用来实现动态加载配置文件。

使用指令让bot修改配置文件或重载配置文件，而无需再重启bot。
## 用法
```python
from plugins.core.yamlLoader import YAMLManager

config = YAMLManager(["config/basic_config.yaml","config/api.yaml","config/controller.yaml"]) #这玩意用来动态加载和修改配置文件
```
然后你可以通过
```python
model=config.api["llm"]["model"]
print(model)
```
访问指定配置文件的指定配置项。
