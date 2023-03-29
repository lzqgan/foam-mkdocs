---
tags: jc教程/群辉, soft
---

[[02-群晖系统]]

一、制作PE盘
1、将U盘插入电脑，运行PE盘制作工具，右下角选择“安装PE到U盘”

2、如图设置，点击“立即安装进U盘”

3、PE盘制作工具生成了两个分区，EFI为PE引导分区，“微PE工具箱”为文件区，将黑群晖引导镜像（img）、DiskImg、DiskGenius（PE版）放入U盘内。

二、引导文件写入SSD
1、将制作好的PE U盘插入蜗牛星际背部USB接口，通电开机，并按F7选择PE U盘启动（BIOS LOGO画面按DEL进入BIOS设置，按F7选择启动设备）。

2、使用DiskGenius，将自带16G SSD内所有分区删除并保存。

3、启动 DiskImg ，驱动器选择机器内置SSD，浏览选择镜像写入（路径、文件名不能有任何中文字符）。
![](https://img-blog.csdnimg.cn/20200226010933750.png)
4、写入完成后，使用DiskGenius（PE自带版本太旧了，一定要用复制进去的DiskGenius），浏览系统内置SSD引导分区文件（ESP），将grub.cfg文件复制到U盘（之后洗白要用）。

5、设备关机，拔出U盘。
三、安装DSM至NAS主机
1、NAS主机安装储存盘， NAS主机连接网线并启动主机（成功的话屏幕会显示Happy Hacking） 。

2、 同一局域网内计算机安装Synology Assistant（群晖助手） 并搜索，图中红圈处会显示“DSM未安装”。

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tYXBndW4uY29tL3dwLWNvbnRlbnQvdXBsb2Fkcy8yMDE5LzAzL2ltYWdlLTUucG5n?x-oss-process=image/format,png)

3、选中NAS主机安装DSM系统，浏览找到pat格式，依照提示安装即可

4、注意一下，这里不要把自动更新打开，也不要开启任何反馈计划。初始化DSM后记得在控制面板中将自动更新彻底关掉，避免系统更新后与引导文件不匹配，造成启动失败。

5、初始化DSM完成，进入桌面后，关机。