---
title: 优化 mpv 播放器的在线视频体验
date: 2025-02-08 11:56:25
updated: 2025-03-13 19:04
tags:
- mpv
- Media Player
---

## 开始之前的一点私货（逃

我的 mpv 自用配置：https://github.com/Yukari0201/mpv-config

联系阅读：
[[Tip]使用yt-dlp增强mpv player流媒体解析能力&解锁登陆用户分辨率](https://www.bilibili.com/read/cv21234242)

## 观前提醒(消歧义)

本篇所讲的播放在线视频的方案为 **mpv** + **yt-dlp**， 

而非 **ff2mpv**、**Play-With-MPV**、**使用 MPV 播放 + mpv-handler** 这样的 扩展/脚本 方案

提到的 扩展/脚本：  
- ff2mpv https://github.com/woodruffw/ff2mpv
- Play-With-MPV https://greasyfork.org/zh-CN/scripts/444056-play-with-mpv
- 使用 MPV 播放（需配合 mpv-handler 使用） https://greasyfork.org/zh-CN/scripts/416271-play-with-mpv

## 目录

- mpv 播放器如何播放在线视频
  - 直接拖放链接
  - 使用内置控制台脚本(console.lua)
  - 命令行用法
- 缓存(cache)配置
- 内置的 ytdl_hook 脚本相关
  - 前提条件
  - ytdl_hook 脚本配置
    - 常规选项部分
    - `--ytdl-raw-options` 部分
    - `script-opts/ytdl_hook.conf` 部分(`--script-opts` 部分)
- 代理相关
  - [推荐] 在 `mpv.conf` 中设置代理
  - 通过环境变量 `http_proxy` 来设置代理
- (补充) 优化 Bilibili 视频的观看体验
  - [推荐] 使用 bilibiliAssert 脚本

## mpv 播放器如何播放在线视频

### 直接拖放链接

将在线视频链接从浏览器地址栏拖到 mpv 播放窗口中即可开始播放。

视频演示：[【软件分享】开源的全平台视频播放器MPV 使用教程 p02](https://www.bilibili.com/video/BV1nQ4y1a7gw?p=2) 的演示  
感谢：[Bilibili@FinnR](https://space.bilibili.com/111138665)

### 使用内置控制台脚本(console.lua)

联系阅读：[[Tip]使用mpv自带控制台脚本console.lua执行输入命令](https://www.bilibili.com/read/cv27512307)

打开 mpv 播放器，使用快捷键 <code>\`</code> 打开内置 console  
然后输入 `loadfile <视频链接>`，并回车，例如：
```
loadfile https://www.bilibili.com/video/BV1qM4y1w716/
```

**注意**：视频链接中不能有特殊字符，如果有，请将视频链接用半角引号(`""` 或 `''`)包裹起来

### 命令行用法

前提条件：你已经将 mpv 的路径添加到了 环境变量 PATH 中

然后命令行输入 `mpv <视频链接>`，并回车，例如：
```
mpv https://www.bilibili.com/video/BV1qM4y1w716/
```
**注意**：视频链接中不能有特殊字符，如果有，请将视频链接用半角引号(`""` 或 `''`)包裹起来

## 缓存(cache)配置

mpv 播放器的缓存(cache)用来提前读取数据，提供更流畅的播放体验，避免播放过程中的卡顿或跳帧（常见原因：网络波动、磁盘延迟）

相关选项参见官方手册：  
https://mpv.io/manual/master/#cache  
https://mpv.io/manual/master/#demuxer

我挑出了几个比较有用的选项，并更改为适用于大部分场景的配置，你可以参考一下  
```ini
# 根据视频是否为是为网络链接来决定是否启用缓存。
# 即：对网络视频启用缓存，对本地视频不启用缓存
cache=auto
# 可选值 <yes|no|auto>(默认auto)

# 将缓存写入内存
cache-on-disk=no
# 可选值 <yes|no>(默认yes)
# yes - 将将缓存写入一个磁盘上的临时文件
# no - 将缓存写入内存

# 最大向后缓存大小(默认 150MiB)
demuxer-max-bytes=150MiB
# 最大允许保留的已播放的内容的数据大小(默认 50MiB)
demuxer-max-back-bytes=50MiB

# 设置10秒缓存滞后时间，可以节省功耗(默认值 0, 即禁用缓存滞后)
demuxer-hysteresis-secs=10
# 官方手册说设置为 10 对大部分情况都有用
# 此选项的意思是：
# 达到 --demuxer-max-bytes 的限制后，直到缓存中剩下多少秒时才重新开始缓冲  
# 这可以显著节省功耗（不启用时，会不停缓冲；启用时，会将视频分成好几段缓冲）
```

注意: `--demuxer-max-back-bytes` 和**向前缓存**不尽相同。  
文字解释起来有点麻烦，我放张图吧...  
![--demuxer-max-back-bytes](--demuxer-max-back-bytes.png)  

## 内置的 ytdl_hook 脚本相关

mpv 可以调用 yt-dlp 来增强网络视频播放能力，这依赖内置脚本 ytdl_hook.lua

### 前提条件

#### "安装" yt-dlp

Windows 用户：  
去 yt-dlp 官方 Github Releases 下载 yt-dlp.exe，将 yt-dlp.exe 放入 mpv.exe 的同路径下 或 系统 PATH 中  
yt-dlp 官方 Github Releases: https://github.com/yt-dlp/yt-dlp/releases

Linux 用户：  
常见的发行版通过包管理器安装即可  
例如 Arch Linux
```
sudo pacman -S yt-dlp
```

其他建议直接看 yt-dlp 的 Wiki：https://github.com/yt-dlp/yt-dlp/wiki/Installation

### ytdl_hook 脚本配置

#### 常规选项部分

参见: https://mpv.io/manual/master/#options-ytdl

```ini
# 启用内置的 ytdl_hook 脚本
ytdl=yes
# 可选值 <yes|no>(默认值: yes)

# 设置直接传递给 youtube-dl 的视频格式/质量，示例即为默认值
ytdl-format=bestvideo+bestaudio/best
# 这部分怎么写应该查看 yt-dlp 的文档
# https://github.com/yt-dlp/yt-dlp#format-selection  
```

**默认的配置已经足够使用，非必要不建议更改**

#### `--ytdl-raw-options` 部分

参见: https://mpv.io/manual/master/#options-ytdl-raw-options

`--ytdl-raw-options` 用于将自定义选项传递给 yt-dlp，可用选项参见: https://github.com/yt-dlp/yt-dlp#usage-and-options  
选项应为选项参数键值成对的方式传递(`<key>=<value>`)，没有参数的选项后面必须加上等号 `=`  
多个键值对之间用半角逗号 `,` 隔开，例如：  
```ini
ytdl-raw-options=write-subs=,force-ipv6=,sub-langs=[zh,en]
```
实际使用时，更推荐使用多个 `--ytdl-raw-options-append`，例如上面的选项也可以写为：
```ini
ytdl-raw-options-append=write-subs=
ytdl-raw-options-append=force-ipv6=
ytdl-raw-options-append=sub-langs=zh,en
```

我挑出了几个比较有用的选项，列在下面：  
**注意**：**不要乱加空格美化**
```ini
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

# 限制选择字幕语言
ytdl-raw-options-append=sub-langs=all
# sub-langs=all 表示选择所有字幕
# 你可以使用正则表达式来限制选择字幕语言，例如：
#ytdl-raw-options-append=sub-langs=ai.*,zh.*,en.*,ja.*
```

[Tips] 你可以命令行运行如下命令导出 Firefox 浏览器的 cookies 为 `cookies.txt`，其他浏览器也同理  
```
yt-dlp --cookies cookies.txt --cookies-from-browser firefox
```

#### `script-opts/ytdl_hook.conf` 部分(`--script-opts` 部分)

mpv 实际上是通过内置的 ytdk_hook 脚本调用 yt-dlp 的，所以类似于其他脚本，它也可以通过在 mpv 设置文件夹的 script-opts 文件夹中新建一个 ytdl_hook.conf 来设置脚本选项

**注意**：`ytdl_hook.conf` 文件的编码应为 UTF-8，换行应为 LF(Unix)

所有可用的选项看官方手册：https://mpv.io/manual/master/#options-ytdl

大部分情况下，**默认的配置已经足够使用，非必要不建议更改**

## 代理相关

听不懂请直接跳过

部分代理软件支持 Tun 方式或 TProxy/Redirect 方式设置透明代理，如果你正在使用，可以跳过此部分

由于 mpv 不会使用系统代理设置，所以如果想要播放某些地域限制的 URL，需要手动设置代理

以下两种方式**选择其中一种**即可

### [推荐] 在 `mpv.conf` 中设置代理

参见:  
https://mpv.io/manual/master/#options-http-proxy  
https://mpv.io/manual/master/#options-ytdl-raw-options

```ini
# 你应该将下面的 http://127.0.0.1:3128 自行更改为你的代理地址
# 我只不过是将官方文档的示例照抄过来了而已

# 让 mpv 使用 http(s) 代理
http-proxy=http://127.0.0.1:3128
# 让 yt-dlp 使用 http(s) 代理
ytdl-raw-options-append=proxy=http://127.0.0.1:3128
# 虽然 yt-dlp 支持 socks，但由于此选项的值会被传递给 mpv，所以还是只能使用 http 代理
```

### 通过环境变量 `http_proxy` 来设置代理

参见: https://mpv.io/manual/master/#environment-variables-http-proxy

经我测试，yt-dlp 也会使用此环境变量设置的代理，所以不必再在 `mpv.conf` 中作其他设置

将环境变量 `http_proxy` 的值自行设置为你的代理地址即可，**只支持 http 类型的代理**，例如 `http://127.0.0.1:3128`

具体设置方式:  
- Linux: 请参考 [ArchWiki](https://wiki.archlinux.org/title/Environment_variables) 或 [Arch Linux 中文维基](https://wiki.archlinuxcn.org/wiki/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)
- Windwos: TODO

## (补充) 优化 Bilibili 视频的观看体验

在读完上述部分后，各位读者可能会遇到一个问题，当 `mpv.conf` 文件中存在如下部分时，如果播放B站视频，会多出一个 `slang`(字幕语言) 为 `danmaku` 的字幕，切换至此字幕会导致卡死
```ini
# 限制选择字幕语言
ytdl-raw-options-append=sub-langs=all
# sub-langs=all 表示选择所有字幕
```

例如下图中，如果切换至 `danmaku` 字幕，mpv 播放器画面会卡死  
![sub-langs=all](sub-langs=all.png) 

原因：`danmaku` 是 xml 格式的 B站弹幕，mpv 无法正常渲染，所以切换过去会卡死

解决方案有两种，先说最简单的一种：  
将上面的内容改为：
```ini
# 限制选择字幕语言
ytdl-raw-options-append=sub-langs=all,-danmaku
# sub-langs=all,-danmaku 表示选择所有字幕，并排除 danmaku 字幕
```

此时字幕列表中便不会有 `danmaku` 字幕，比如下图：  
![sub-langs=all,-danmaku](sub-langs=all,-danmaku.png)

### [推荐] 使用 bilibiliAssert 脚本

如果你想看到 B站的弹幕，那么可以使用 MPV-Play-BiliBili-Comments(bilibiliAssert) 脚本，即第二种解决方案

使用方式：  
访问 MPV-Play-BiliBili-Comments 的 [Github 项目地址](https://github.com/itKelis/MPV-Play-BiliBili-Comments)，点击右侧的绿色的 `Code`，然后点击 `Download ZIP` 下载项目源码(下载下的文件名一般为 `MPV-Play-BiliBili-Comments-main.zip`)  
然后解压压缩文件，并将里面的 `bilibiliAssert` 文件夹解压至 `<你的 mpv 配置文件夹>\scripts\`

最终你的 mpv 配置文件夹应该类似于下面所示  
```
~/.config/mpv/ 或 portable_config/
├── script-opts/
│   └── *.conf (你的脚本的配置文件)
├── scripts/
│   ├── bilibiliAssert/
│   │   ├── Danmu2Ass.exe
│   │   ├── Danmu2Ass.py
│   │   └── main.lua
│   └── *.lua (你的其他脚本)
│── shaders/
│   └── *.glsl (你的着色器)
├── input.conf
└── mpv.conf
```

如果需要定制化弹幕样式，请自行查看项目 Readme
