---
title: "【Obsidian】将 B 站视频和笔记保存到本地，无需安装插件，浏览器内使用，win、mac 皆可 - 哔哩哔哩"
alias: 
  - "【Obsidian】将 B 站视频和笔记保存到本地，无需安装插件，浏览器内使用，win、mac 皆可 - 哔哩哔哩"
created-date: 2023-03-22T16:08:01+0800
type: Simpread
banner: "https://i0.hdslb.com/bfs/article/b39273805c6b5d54ba151da59b9179c737e1f70b.jpg "
banner_icon: 🔖
tag: 
idx: 6
banner_y: 0.5
---

# 【Obsidian】将 B 站视频和笔记保存到本地，无需安装插件，浏览器内使用，win、mac 皆可 - 哔哩哔哩

> [!example]- [🌐外部链接](<https://www.bilibili.com/read/cv20159517>)    
> URI:: [🌐](<https://www.bilibili.com/read/cv20159517>) 
> intURI:: [🧷内部链接](<https://www.bilibili.com/read/cv20159517>)

%%
> [!example]+ **Comments**  
> ```dataview
> TABLE 
>     WITHOUT ID
>     link(Source, dateformat(date(Source), "yyyy-MM-dd")) as Date___, 
>     regexreplace(rows.Comments,"^@@\[\[.+?\]\]\s","") as "Comments"
> FROM "journals"
> WHERE  contains(cmnt, this.file.name)
> FLATTEN cmnt as Comments
> WHERE contains(Comments, this.file.name)
> GROUP BY file.link as Source
> SORT rows.file.day desc
> ```
>  **Description**:: 本文分享一个操作简单的方法，可以将 B 站视频和个人笔记保存成 markdown 格式的学习清单并下载到本地，保留原来的笔记格式外，还将会自动分割整合不同分 P 下的笔记内容到一起，适合搭配 Obsidian ......
%%

> [!md] Metadata  
> **标题**:: [【Obsidian】将 B 站视频和笔记保存到本地，无需安装插件，浏览器内使用，win、mac 皆可 - 哔哩哔哩](https://www.bilibili.com/read/cv20159517)  
> **日期**:: [[2023-03-22]]  

## Annotations


> [!srhl2] [[SR6@【Obsidian】将 B 站视频和笔记保存到本地，无需安装插件，浏览器内使用，win、mac 皆可 - 哔哩哔哩|📄]] <mark style="background-color: #ffeb3b">Highlights</mark>   
> 1. 进入视频页
> 
> 2. 如果希望同时保存个人笔记，则需提前打开笔记的内容面板
> 
> 3. 打开 “开发者工具（DevTools）”（快捷键 F12 / 右键页面 - 检查 / 设置 - 更多工具 - 开发者工具）
> 
> 4. 将开发者工具切换到 “控制台（Console）” 面板，可选择清除一下控制台（快捷键 Ctrl+L）
> 
> 5. 复制下面代码到控制台
> 
> ```
> var script = document.createElement("script");  
> script.type = "text/javascript";  
> script.src = "https://cdn.jsdelivr.net/gh/Jayvin-Leung/script@main/Ji_iL.beta.js";  
> document.head.appendChild(script);  
> 
> ```
> 
> github+jsdelivr（国外）：如遇网络不稳定可能无法正常使用，可尝试翻墙或替换为以下代码
> 
> ```
> var script = document.createElement("script");  
> script.type = "text/javascript";  
> script.src = "https://gitee.com/Jayvin_Leung/script/releases/download/v1.0/Ji_iL.beta.js";  
> document.head.appendChild(script);
> ```
> ^sran-1679472518015

