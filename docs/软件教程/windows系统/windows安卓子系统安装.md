----

[[03-windows]]

1.[[windows安卓子系统安装]]   [下载地址](https://store.rg-adguard.net/)> 右边的选项卡选择 Slow 然后将之前的网址粘贴到搜索框，点击右边的对号 √ 进行搜索
2.apk安装   微软商店：**apk安装器**    **WSA工具箱**
3.[[配置Clash软件的TUN-TAP虚拟网卡]]

-----
> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/NEKOic/article/details/123454682)

### 目录

*   [Windows 11 安卓子系统 (Sub System for Android™) 安装问题汇总](#Windows_11__Sub_System_for_Android__1)
*   *   [准备工作](#_4)
    *   *   *   [== 建议用手机打开本文，因为后面涉及到多次系统重启 ==](#_6)
            *   [1. 检查你的电脑是否开启了 CPU 虚拟化功能](#1_CPU_7)
            *   [2. 开启 Hyper-V 和 虚拟机平台功能](#2__HyperV___14)
            *   [3. 安装安卓子系统](#3__34)
            *   [4. 安装安卓程序 (apk 包)](#4_apk_59)

Windows 11 安卓子系统 (Sub System for Android™) 安装问题汇总
=================================================

前段时间，微软开放了所有美区用户的安卓子系统下载通道，但目前其他国家和地区还没有开放下载，如果你现在就想尝试使用安卓子系统可以参考本文章，本文汇总了我在安装该系统时遇到的问题及其解决办法，希望能帮到你。

准备工作
----

#### 建议用手机打开本文，因为后面涉及到多次系统重启

#### 1. 检查你的电脑是否开启了 CPU [虚拟化](https://so.csdn.net/so/search?q=%E8%99%9A%E6%8B%9F%E5%8C%96&spm=1001.2101.3001.7020)功能

1.  右键单击 Windows 图标，选择任务管理器
2.  点击 [性能] 选项卡，查看 CPU 性能详情
3.  检查图示处是否开启了虚拟化功能  
    ![](https://img-blog.csdnimg.cn/4bbedcf9c233405fa61885f85fcbc0a8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)
4.  已开启的话直接进行下一步，未开启则重启电脑，在出现开机 logo 时按特定按键（一般为 F2 或 Del）进入主板 BIOS 修改设置。不同主板设置的位置不同，具体在哪请查找相关教程。

#### 2. 开启 [Hyper-V](https://so.csdn.net/so/search?q=Hyper-V&spm=1001.2101.3001.7020) 和 虚拟机平台功能

1.  打开设置或直接在全局搜索中，搜索关键词 [功能]，找到 [启用或关闭 Windows 功能]  
    ![](https://img-blog.csdnimg.cn/011d8dbdad5d4ebe800325349398a506.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)
2.  勾选 Hyper-V、虚拟机监控程序平台、虚拟机平台，点击 [确定] 后 重启  
    ![](https://img-blog.csdnimg.cn/ed167e37d43e45c4b6241b96d7b7c1b5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_18,color_FFFFFF,t_70,g_se,x_16)

> 若你的系统不是 win11 专业版，此处可能没有 Hyper-V 这个选项，但可以通过控制台脚本进行安装。  
> 解决办法是新建一个文本文件，复制下面的代码粘贴到文件里，修改文件名为 Hyper-V.cmd，注意文件后缀名修改为 .cmd

```
pushd "%~dp0"  
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt  
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"  
del hyper-v.txt  
Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL

```

> 确保你开启了 [显示文件扩展名] 的功能  
> ![](https://img-blog.csdnimg.cn/125f2408fa134a58b2bc2e363d6e8a31.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)  
> 右键点击创建好的脚本文件，选择以管理员身份运行，这里安装时间较长，请耐心等待，安装完成后提示是否重启，输入 y 回车后重启电脑进行下一步

#### 3. 安装安卓子系统

首先请开启开发者模式，所有设置都一样，在全局搜索都能搜得到  
这里你可以先打开浏览器，输入下面的网址到地址栏，点击 [GET] 跳转到 win 11 应用商店，尝试是否能直接安装。

> https://www.microsoft.com/en-us/p/windows-subsystem-for-android-with-amazon-appstore/9p3395vx91nr

![](https://img-blog.csdnimg.cn/a3524c53513a4285ae98c8d9e257fab0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)![](https://img-blog.csdnimg.cn/5507153a60464b16ad4a995a4e618973.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)  
如果你的电脑符合要求，应该是能直接安装的，我的电脑没装固态所以不能在这安装，如果不能请接着往下看

> 打开下面的地址  
> https://store.rg-adguard.net/  
> 右边的选项卡选择 Slow 然后将之前的网址粘贴到搜索框，点击右边的对号 √ 进行搜索  
> ![](https://img-blog.csdnimg.cn/f6be8c635a504163974cee4fd016fae2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)  
> 找到搜索结果中的安卓子系统，点击进行下载  
> ![](https://img-blog.csdnimg.cn/257ede7905f847b188cd6c8a7b792cd8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)  
> 下载完成后右键点击 Windows 图标，选择 Windows 终端（管理员），使用 `Add-AppxPackage` 命令进行安装，指令如下：  
> Add-AppxPackage 后面是安卓子系统安装文件的路径，根据你自己的下载位置填写，安装完成后需要重启

```
Add-AppxPackage D:\Download\FireFox\MicrosoftCorporationII.WindowsSubsystemForAndroid_2203.40000.1.0_neutral_~_8wekyb3d8bbwe.Msixbundle

```

安装完成后在开始菜单能找到我们安装的子系统和亚马逊应用商店，打开安卓子系统，进入到设置页面  
![](https://img-blog.csdnimg.cn/b3d22fe9bd6e406e8c248419e1c6a09a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)

#### 4. 安装安卓程序 (apk 包)

Windows 应用商店已经有 apk 安装器了，我尝试了几个之后推荐一个好用的  
![](https://img-blog.csdnimg.cn/d2bafda7d0ee43d78e001591ecb1aeb4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATkVLT--8gQ==,size_20,color_FFFFFF,t_70,g_se,x_16)  
安装完成后等待程序准备完成，选择你的 apk 文件然后就可以安装了，不想安卓子系统开机自启可以去开机启动项里把安卓子系统的开机启动关闭
