---
title: 优化 mpv 播放器的在线视频体验
date: 2025-02-08 11:56:25
tags:
- mpv
- Media Player
---

## 开始之前的一点私货（逃

我的 mpv 自用配置：https://github.com/Yukari0201/mpv-config

联系阅读：
[[Tip]使用yt-dlp增强mpv player流媒体解析能力&解锁登陆用户分辨率](https://www.bilibili.com/read/cv21234242)  
本文是对此篇文章的补充

## 观前提醒(消歧义)

本篇所讲的播放在线视频的方案为 **mpv** + **yt-dlp**， 

而非 **ff2mpv**、**Play-With-MPV**、**使用 MPV 播放 + mpv-handler** 这样的 扩展/脚本 方案

提到的 扩展/脚本：  
- ff2mpv https://github.com/woodruffw/ff2mpv
- Play-With-MPV https://greasyfork.org/zh-CN/scripts/444056-play-with-mpv
- 使用 MPV 播放（需配合 mpv-handler 使用） https://greasyfork.org/zh-CN/scripts/416271-play-with-mpv

## 目录
- 在正文开始前讲一下 mpv 播放器如何播放在线视频

## 在正文开始前讲一下 mpv 播放器如何播放在线视频

### 直接拖链接

请参考 [【软件分享】开源的全平台视频播放器MPV 使用教程 p02](https://www.bilibili.com/video/BV1nQ4y1a7gw?p=2) 的演示

### 内置控制台脚本(console.lua)用法

联系阅读：[[Tip]使用mpv自带控制台脚本console.lua执行输入命令](https://www.bilibili.com/read/cv27512307)

打开 mpv 播放器，使用快捷键 **`** 打开内置 console  
然后输入下面的内容，并回车
```
loadfile <视频链接>
```
例如：
```
loadfile https://www.bilibili.com/video/BV1qM4y1w716/
```

注意：视频链接中不能有特殊字符，如果有，请将视频链接用半角引号( "" 或 '' )包裹起来

### 命令行用法

前提条件：你已经将 mpv 的路径添加到了 环境变量 PATH 中
```
mpv <视频链接>
```
注意：视频链接中不能有特殊字符，如果有，请将视频链接用半角引号( "" 或 '' )包裹起来

## 缓存(cache) 部分

mpv 播放器的缓存(cache)用来提前读取数据，提供更流畅的播放体验，避免播放过程中的卡顿或跳帧（常见原因：网络波动、磁盘延迟）

相关选项参见官方手册：  
https://mpv.io/manual/master/#cache  
https://mpv.io/manual/master/#demuxer

我挑出了几个比较有用的选项，并更改为适用于大部分场景的配置，你可以参考一下  
```
cache=auto
cache-on-disk=no
demuxer-max-bytes=150MiB
demuxer-max-back-bytes=50MiB
demuxer-hysteresis-secs=10
```

### 接下来，一一讲解这些选项

> `--cache=auto`  

可选值 <`yes`|`no`|`auto`>(默认 `auto`)  
`yes` - 对所有视频启用缓存  
`no` - 对所有视频不启用缓存  
`auto` - 可以简单理解为：根据视频是否为是为网络链接来决定是否启用缓存。即：对网络视频启用缓存，对本地视频不启用缓存

我建议保持默认值 `auto`，除非你的磁盘掉速才建议使用 `yes`

> `--cache-on-disk=no`

可选值 <`yes`|`no`>

`yes` - 将缓存写入一个磁盘上的临时文件(由 `--demuxer-cache-dir=<path>` 指定)  
`no` - 将缓存写入内存  

> `--demuxer-max-bytes=150MiB`  
> `--demuxer-max-back-bytes=50MiB`

`--demuxer-max-bytes` 最大向后缓存大小，默认 150MiB

`--demuxer-max-back-bytes` 最大允许保留的已播放的内容的数据大小，默认 50MiB  
注意！这和**向前缓存**不尽相同。  
解释起来有点麻烦，我放张图吧...  
![--demuxer-max-back-bytes]()  

> `--demuxer-hysteresis-secs=10`

达到 `--demuxer-max-bytes` 的限制后，直到缓存中剩下多少秒时才重新开始缓冲  
这可以显著节省功耗（不启用时，会不停缓冲；启用时，会将视频分成好几段缓冲） 

默认值：0 （即禁用缓存滞后）  

官方手册说设置为 10 对大部分情况都有用  

## 内置的 ytdl_hook 脚本相关

mpv 可以调用 yt-dlp 来增强网络视频播放能力，这依赖内置脚本 ytdl_hook.lua

### 前提条件

#### "安装" yt-dlp

Windows 用户：  
去 yt-dlp 官方 Github Releases 下载 yt-dlp.exe，将 yt-dlp.exe 放入 mpv.exe 的同路径下即可  
yt-dlp 官方 Github Releases: https://github.com/yt-dlp/yt-dlp/releases

Linux 用户：  
建议直接看 yt-dlp 的 Wiki：https://github.com/yt-dlp/yt-dlp/wiki/Installation

### ytdl_hook 脚本配置

#### 常规选项部分

参见 https://mpv.io/manual/master/#options-ytdl

```
ytdl=yes
# 启用内置的 ytdl_hook 脚本
# <yes|no>(默认值: yes)
# no 表示不启用

ytdl-format = bestvideo+bestaudio/best
# 设置直接传递给 youtube-dl 的视频格式/质量，示例即为默认值
# 这部分怎么写应该查看 yt-dlp 的文档，我记得是在这里 https://github.com/yt-dlp/yt-dlp#format-selection  
```
**默认的配置已经足够使用，非必要不建议更改**

#### --ytdl-raw-options 部分

`--ytdl-raw-options` 用于将自定义选项传递给 yt-dlp，可用选项参见 https://github.com/yt-dlp/yt-dlp#usage-and-options  
选项应为选项参数键值成对的方式传递(`<key>=<value>`)，没有参数的选项后面必须加上等号 `=`  
多个键值对之间用半角逗号","隔开，例如：  
```
ytdl-raw-options=write-subs=,force-ipv6=,sub-langs=[zh,en]
```
当然，实际使用时，更推荐使用多个 `--ytdl-raw-options-append`，如下：
```
ytdl-raw-options-append=write-subs=
ytdl-raw-options-append=force-ipv6=
ytdl-raw-options-append=sub-langs=zh,en
```

我挑出了几个比较有用的选项，列在下面：  
**注意**：**不要乱加空格美化**
```
# 从浏览器导入 cookies，解锁已登录账户的分辨率
ytdl-raw-options-append=cookies-from-browser=firefox
# 示例为导入 Firefox 的 cookies
# 你可以将 firefox 换成你正在使用的其它浏览器名，支持 brave, chrome, chromium, edge, firefox, opera, safari, vivaldi

# 也可以导入文件的 cookies，只支持绝对路径
#ytdl-raw-options-append=cookies=cookies.txt

# 如果URL同时指向视频和播放列表（例如B站分p视频），解析为播放列表
ytdl-raw-options-append=yes-playlist=

# 解析字幕
ytdl-raw-options-append=write-subs=

# 限制字幕语言，可以使用正则表达式
ytdl-raw-options-append=sub-langs=ai.*,zh.*,en.*
# 其实不用这个选项也足以应对大多数场景
# 放在这里只是作为演示，以及照顾一下需要的用户
```

[Tips] 你可以命令行运行如下命令来导出 Firefox 浏览器的 cookies 为 `cookies.txt`，其他浏览器也同理  
```
yt-dlp --cookies cookies.txt --cookies-from-browser firefox
```

#### script-opts/ytdl_hook.conf 部分（--script-opts 部分）

mpv 实际上是通过内置的 ytdk_hook 脚本调用 yt-dlp 的，所以类似于其他脚本，它也可以通过在 mpv 设置文件夹的 script-opts 文件夹中新建一个 ytdl_hook.conf 来设置脚本选项

**注意**：ytdl_hook.conf 文件的编码应为 UTF-8，换行应为 LF(Unix)

所有可用的选项看官方手册：https://mpv.io/manual/master/#options-ytdl

大部分情况下，**默认的配置已经足够使用，非必要不建议更改**

## 代理相关

听不懂请直接跳过

TODO...

