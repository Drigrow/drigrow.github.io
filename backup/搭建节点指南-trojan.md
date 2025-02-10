这篇内容是大致从之前的博客上搬过来的，讲一下如何快速自建一个trojan节点。

trojan前几年因为伪装效果好有一定受众，现在因为墙可以检测tls-in-tls的特征(trojan有)，所以部分地区无法使用，但是仍然有相当一部分地区可以使用，那么，希望这篇文章能帮到这些人们^^

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

### 安装trojan
这个步骤我使用easytrojan项目：[https://github.com/eastmaple/easytrojan](https://github.com/eastmaple/easytrojan)

×可选：
在开始之前，升级系统包
对于RHEL(Centos/Redhat等系统):
```bash
yum update
```
对于Debian/Ubuntu:
```bash
apt update && apt upgrade
```

在登录服务器后，输入这个命令安装trojan:
```bash
curl https://raw.githubusercontent.com/eastmaple/easytrojan/main/easytrojan.sh -o easytrojan.sh && chmod +x easytrojan.sh && bash easytrojan.sh password
```
其中，替换`password`为你自己的密码。

耐心等待一会，应该会出现trojan的连接参数。类似：
```txt
地址：<server>.nip.io
端口：443
密码：password
ALPN: h2/http1.1
```

×如果服务器开启了防火墙，应当至少打开`80/tcp`和`443/tcp`两个端口，方法参见[easytrojan仓库](https://github.com/eastmaple/easytrojan?tab=readme-ov-file#%E6%94%BE%E8%A1%8C%E7%AB%AF%E5%8F%A3)，或自行上网查找。

### 连接
clash内核用户请自行下载任意样本配置文件，如[config.yaml](https://github.com/MetaCubeX/mihomo/blob/Meta/docs/config.yaml)等等，自行修改trojan部分参数后，导入代理软件。
v2raym用户在v2rayn顶部导航栏找到`添加服务器-添加trojan服务器`后自行输入参数。
之后的步骤就是正常代理上网了～