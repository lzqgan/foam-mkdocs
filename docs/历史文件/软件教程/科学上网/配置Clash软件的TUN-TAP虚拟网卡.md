---
tag : 科学上网
---
[[08-科学上网]]

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [uzbox.com](https://uzbox.com/tech/clash-atp.html)

> 有些时候，玩游戏或者使用某个特定软件时候需要用到外网 IP，目前比较常见的 V2ray，或者 Shadowsocks 等代理工具，只能实现网页访问的代理功能。

浏览器之类的应用都是使用系统代理访问的，有些时候一些非系统代理应用，例如玩游戏或者使用某个特定软件需要特定 IP 时，目前比较常见的 V2ray 或者 Shadowsocks 等代理工具，只能实现网页访问的代理功能。如何实现网卡层访问？接下来详细介绍 [Clash for Windows](https://uzbox.com/tag/clash-for-windows "Clash for Windows") 的 [TAP 虚拟网卡](https://uzbox.com/tag/tapxuniwangka "TAP虚拟网卡")功能。

首先我们先了解一下，什么是 Clash for Windows 的 TAP 虚拟网卡功能。

### TUN/TAP 模式

在 Windows 中对于不遵循系统代理的软件，TAP 模式可以接管其流量并交由 CFW 处理。对于 0.13.8 及以后版本，更推荐使用 TUN 模式。安装虚拟网卡功能后可以实现全局代理！

### 配置 TUN/TAP 模式

当前 Clash for Windows 最新版本是 V0.18.7，推荐使用 TUN 模式

首先下载最新版本的 Clash for Windows，具体可以参考：[Clash for Windows 中文汉化教程](https://uzbox.com/tech/clash.html)

接下来安装 TUN 模式或者是 TAP 模式。

#### TUN 模式

首先安装好汉化后的 Clash for Windows 最新版本后，打开软件！

![](https://uzbox.com/wp-content/uploads/2021/11/2021110818335132-e1636396513147-1024x732.png)

在常规 (General) 页面中找到服务模式(Service Mode)，点击后面的管理(Manage)。点击之后会弹出小窗口。

![](https://uzbox.com/wp-content/uploads/2021/11/202111081838143.png)

点击安装后，软件会自动关闭然后会重新启动，安装成功后，服务模式后面的灰色地球的图标会点亮变成绿色。图标变成绿色后，TUN 模式安装成功！

接下来点击设置 (Settings), 在 Mixin 混合配置(Profile Mixin) 下面找到 YAML，点击后面的编辑。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110818420952-1024x732.png)

将下列代码添加到 YAML 中：

**注意：下列代码中的空格缩进，一定要复制完整代码，不要删除代码前面的空格。**

```
mixin: 
   hosts:
     'mtalk.google.com': 108.177.125.188
     'services.googleapis.cn': 74.125.203.94
     'raw.githubusercontent.com': 151.101.76.133
   dns:
     enable: true
     default-nameserver:
       - 223.5.5.5
       - 1.0.0.1
     ipv6: false
     enhanced-mode: redir-host #fake-ip
     nameserver:
       - https://dns.rubyfish.cn/dns-query
       - https://223.5.5.5/dns-query
       - https://dns.pub/dns-query
     fallback:
       - https://1.0.0.1/dns-query
       - https://public.dns.iij.jp/dns-query
       - https://dns.twnic.tw/dns-query
     fallback-filter:
       geoip: true
       ipcidr:
         - 240.0.0.0/4
         - 0.0.0.0/32
         - 127.0.0.1/32
       domain:
         - +.google.com
         - +.facebook.com
         - +.twitter.com
         - +.youtube.com
         - +.xn--ngstr-lra8j.com
         - +.google.cn
         - +.googleapis.cn
         - +.gvt1.com
   tun: 
     enable: true
     stack: gvisor
     dns-hijack:
       - 198.18.0.2:53
     macOS-auto-route: true
     macOS-auto-detect-interface: true # 自动检测出口网卡

```

然后点击右下角存盘图标，保存当前设置。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819073266-1024x731.png)

保存之后，返回到主界面，将混合配置 (Mixin) 后面的开关启用，变成绿色后，TUN 模式成功开启。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819091946-1024x735.png)

TUN 模式成功开启后，在连接菜单下查看，连接状态中都包含了 TUN 的标志。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819163012-1024x732.png)

好了 TUN 模式已经开启成功了，不过有一些软件或者游戏 TUN 模式还是无法满足功能需求，下面介绍 TAP 虚拟网卡。

#### TAP 模式

首先需要安装 TAP 虚拟网卡，点击常规 (General) 页面中 TAP 网络适配器 (TAP Device) 选项后面的管理 (Manage) 按钮，在弹出对话框中点击安装 (Install) 将会安装 TAP 网卡，TAP 网卡用于接管系统流量。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819270245-1024x738.png)

安装完成后，可以在 Windows 系统的网络连接中看到名为 cfw-tap 的网卡，此时的网卡还是未连接状态。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819295499-1024x619.png)

现在存在一个 Clash 的网卡是在活动状态，如果你之前安装了 TUN 模式，需要先卸载 TUN 模式后，才能安装 TAP 模式。卸载 TUN，在常规中点击服务模式，然后点击卸载就可以了，卸载后，服务模式后面的地球图标变成灰色，就表示卸载成功了。

TAP 模式安装成功后需要启动 TAP 模式。启动 TAP 模式和之前启动 TUN 模式一样，都需要重新编辑 YAML。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110818420952-1024x732.png)

将下面代码添加到窗口里，点击右下角存盘标志保存文件。

```
mixin: 
  dns:
    enable: true    
    enhanced-mode: redir-host
    listen: :53
    nameserver: 
      - https://doh.dns.sb/dns-query
      - https://dns.adguard.com/dns-query
      - https://cdn-doh.ssnm.xyz/dns-query
      - 119.29.29.29 #腾讯
      - 223.5.5.5 #阿里

```

之后返回到常规中，将混合配置后面的开关拨动，激活 TAP 模式，在网络连接中查看 cfw-tap 网卡的模式，已经成功被激活了。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110819574119-1024x610.png)

此时的 cfw-tap 网卡上已经有流量流入流出了。

![](https://uzbox.com/wp-content/uploads/2021/11/2021110820004256.png)

现在已经可以通过 cfw-tap 网卡正常访问了！

Clash 配置文件错误检测：[https://clash.skk.moe/](https://clash.skk.moe/)

警告：本网站仅提供各位软件的技术交流，请在合理合法的范围内使用。严禁用于违法用途。