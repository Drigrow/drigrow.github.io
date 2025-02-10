这篇内容讲一下如何快速自建一个vmess节点。

上一篇trojan的虽然简单，但是因为有`tls-in-tls`特征，某些地区会被针对，所以这篇文章写一个不会被这个方式针对的代理

### 准备工作
* 一台海外服务器
* 一台电脑
*  脑子和手

## 登录服务器
在你购买服务器的商家页面，或者发送给你的邮件里面，一般会包含你服务器的以下信息：
* IP地址
* 用户名(一般为root)
* 密码
* （可能有）端口

如果有端口的，可能是买到了nat机（新手别碰）

对于新手来说，应该没有专用的ssh工具（有的话这段就不用看了，自行登录）

登录过程：

- 打开cmd(win+R之后输入cmd)
- 输入以下命令：
```bash
ssh root@<server>
```
如果有端口的，在语句末尾加上 `-p <port>`
将`<Server>`等替换为自己的服务器信息，回车，应该会问接受指纹(fingerprint)，输入yes，之后输入密码。
×注意，输密码的时候密码一般不会显示，输入完成后回车就好。如需要复制粘贴来密码，尽量不要用`Ctrl+C`粘贴（可能有问题），可以尝试复制后右键cmd粘贴。

### 安装x-ui
参见：[https://github.com/vaxilu/x-ui](https://github.com/vaxilu/x-ui)
方法：
登录服务器后，输入:
···bash
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```
安装x-ui，这里更改的端口/用户名/密码自行记住。
确认端口开放（防火墙放行端口）后，就可以进入x-ui面板了。如果有节点的话，请科学打开面板，如果没有，建议使用ssh隧道加密面板。（原因： 没加密之前是明文的，有泄漏风险）
ssh隧道代码:
```bash
ssh -L <port>:<Server>:8<port> <user>@<server> -N
```
替换服务器信息后新开一个cmd页面，输入，然后访问：
···txt
htp://localhost:<port>
```
没有做ssh隧道的，直接访问：
```txt
http://<server>:"<port>
```

### 打开面板
打开面板网址，输入用户名，密码（之前设置的）进入面板。
找到入站列表，打开。
点击页面上的+号，添加一个vmess节点，在传输方式（网络）那里，将`tcp`改为`ws`，路径随便填一个，可以把用户uuid的前一小段复制过来，注意/不要删掉）

### 连接
可以通过`操作`调出二维码，扫描添加，或者`详细信息`里面找到分享连接导入。clash用户可以自行编写配置文件或者使用订阅节点转换。
险些这么多吧，有空了再加内容。

### 连接
clash内核用户请自行下载任意样本配置文件，如[config.yaml](https://github.com/MetaCubeX/mihomo/blob/Meta/docs/config.yaml)等等，自行修改trojan部分参数后，导入代理软件。
v2raym用户在v2rayn顶部导航栏找到`添加服务器-添加trojan服务器`后自行输入参数。
之后的步骤就是正常代理上网了～