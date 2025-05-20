---
title: 为 mpv 播放器添加长按倍速功能
tags:
  - mpv
  - Media Player
categories:
  - Media Player
  - mpv
---

## 观前提醒

本教程依赖于 `inputevent.lua`
https://github.com/natural-harmonia-gropius/input-event

## 让我们开始叭

### “安装”inputevent.lua

访问 [input-event 项目地址](https://github.com/natural-harmonia-gropius/input-event)，下载 `inputevent.lua`，并将此文件放在你的 mpv 配置文件夹的 `scripts` 目录中

**Windows** 用户的 mpv 配置文件夹的路径一般为 `%APPDATA%\mpv` 或 `mpv.exe` 同路径的 `portable_config`

**Linux** & **macOS** 用户的 mpv 配置文件夹的路径一般为 `~/.config/mpv`

最终你的 mpv 配置文件夹的内容应该类似于下面所示：
```
~/.config/mpv/ 或 %APPDATA%\mpv\ 或 portable_config\
├── script-opts/
│   └── xxx.conf - (你的脚本的配置文件)
├── scripts/
│   ├── xxx.lua - (你的其他脚本)
│   └── inputevent.lua
├── shaders/
│   └── xxx.glsl - (你的着色器)
├── input.conf
└── mpv.conf
```

### 配置 input.conf

在你的 `input.conf` 中写入下面几行，并保存
```ini
# 长按右方向键倍速播放，释放恢复
RIGHT seek 5                            #event: click
RIGHT no-osd set speed 2                #event: press
RIGHT ignore                            #event: release
```

这样就可以长按 `右方向键` 实现2倍速播放视频啦～

同时，单击 `右方向键` 仍旧是 mpv 默认的快进5秒，并没有影响到默认快捷键

## 完结撒花~

### 结束后还要说的事情

`inputevent.lua` 脚本是对 mpv 的 `input.conf` 做了增强，不仅能实现本文所讲的功能，还能自由搭配，实现更多功能，详情请参考官方文档：
https://github.com/natural-harmonia-gropius/input-event

我期待各位配置出独一无二只属于你自己的快捷键，到时候别忘了分享一下哦～

### 一点私货（逃～

我的 mpv 自用配置：https://github.com/Yukari0201/mpv-config
