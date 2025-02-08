今天晚上折腾了一会的项目。
### 问题发现
是因为手上有一台akile香港的机子，流量和带宽都很不错，只是线路绕美，但是我有专线中转，所以没什么问题。延迟也非常理想。唯一，美中不足的是：

**香港地区解锁不了ChatGPT!**

这时候我发现我手上有一个[webshare](https://dashboard.webshare.io/)买来的socks&http代理，美国双isp的（也不知道为什么卖这么便宜，250GB每月只要US$8一年）
### 解决思路
那么，就有了一个想法：我在我香港的机子上面做一个出站分流，指向chatgpt的流量走socks代理，其余流量直连。
### 解决方法
经过认真（确信）分析，只需要更改xray的部分设置就可以达到这个效果。参考：[https://linux.do/t/topic/157378](https://linux.do/t/topic/157378)
以下是步骤：

- 登录x-ui面板
- 在左侧导航栏中找到 `面板设置` 类似选项
- 找到Xray设置

接下来，先把里面的json代码复制出来保存一份，作为备份。接着，开始设置。

在出站部分，也就是 `outbounds`，我们添加一个出站方式:
```json
{
  "tag": "SOCKS1",
  "protocol": "socks",
  "settings": {
    "servers": [
      {
        "address": "addr",
        "port": 1,
        "users": [
          {
            "user": "usr",
            "pass": "pwd"
          }
        ]
      }
    ]
  }
}
```
以上是一个socks代理的默认格式，要用http代理的只用更改`protocol`一项至`http`即可。`tag`可以任意填写，自己记住就行。在其中填写好代理（地址+端口+用户名+密码），可以进入下一步了。

接着，在路由部分，也就是`routing`，我们添加一个路由规则
```json
{
    "type": "field",
    "domainMatcher": "hybrid",
    "domain": [
      "chatgpt.com",
      "openai.com",
      "geosite:openai"
    ],
    "outboundTag": "SOCKS1"
  }
```
其中保持`outboundTag`与先前设置的代理的`tag`一致即可。

然后就可以保存配置，重启xray+面板来测试啦~

如果有问题可以先问gpt，可能是格式之类的问题，或者本身代理的问题，再有不懂的欢迎留言。

同理，可以添加其他不同的分流，比如根据服务器端口不同走不同代理等等，今天这个只是很简单的解锁了chatgpt而已，更多的大家可以继续探索讨论。