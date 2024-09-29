---
title: Arch Linux 安装和配置 Fcitx5 输入法
date: 2023-12-09 18:11:39
tags:
- Arch
- Fcitx5
- GNOME
---

桌面环境：
GNOME(Wayland)  
本教程也适用于 x11

## 安装 Fcitx5  + 中文插件
```
sudo pacman -S fcitx5-im fcitx5-chinese-addons
```

## 设置环境变量
```
sudo gedit /etc/environment
```
（你可以将 gedit 换为其他文本编辑器，例如 vim
```
sudo vim /etc/environment
```
在文件末尾写入以下几行
```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

**注销并重新登录**后，其实就已经可以使用输入法了喵～  
（按 `Ctrl+空格` 即可激活输入法喵～

不过强烈建议继续进行接下来的配置喵～

## [推荐] 安装词库

安装官方存储库中的 fcitx5-pinyin-zhwiki
```
sudo pacman -S fcitx5-pinyin-zhwiki
```

安装 archlinuxcn 存储库中的 fcitx5-pinyin-moegirl
```
sudo pacman -S fcitx5-pinyin-moegirl
```
如果不使用 archlinuxcn 仓库，可以从 AUR 安装  
例如使用 paru 作为 AUR helper 时
```
paru -S fcitx5-pinyin-moegirl
```

这两个词库一般足以应付日常使用了  
如果你还不满意...  
可以...
- 启用云拼音（快捷键 `Ctrl+Alt+Shift+C` ）
- 查找更多词库...
```
paru -Ss fcitx5-pinyin
```

P.S. 我比较推荐安装 `aur/fcitx5-pinyin-custom-pinyin-dictionary`  
由 [@wuhgit/CustomPinyinDictionary](https://github.com/wuhgit/CustomPinyinDictionary) 维护
```
paru -S fcitx5-pinyin-custom-pinyin-dictionary
```

## 安装 Input Method Panel 扩展

如果不安装，可能无法在 GNOME 的活动界面显示输入法窗口（例如搜索框）

### 方法一、[推荐] 安装 AUR 软件包 gnome-shell-extension-kimpanel-git

```
paru -S gnome-shell-extension-kimpanel-git
```

然后在“扩展”中启用 "Kimpanel GNOME Shell"

### 方法二、从 GNOME Shell Extensions 网站安装

#### 安装前的准备

1. 安装 gnome-browser-connector
```
sudo pacman -S gnome-browser-connector
```

2. 可能可选(?)安装浏览器扩展  
参见: https://wiki.gnome.org/action/show/Projects/GnomeShellIntegration/Installation#Distro_packages

#### 安装 Kimpanel GNOME Shell 扩展
访问 GNOME Shell Extensions 网站，安装并启用 Input Method Panel 扩展即可  
https://extensions.gnome.org/extension/261/kimpanel/

## 最后就可以开心打字了喵～

打字愉快喵～

有兴趣可以参考 [ArchWiki](https://wiki.archlinux.org/title/Fcitx5) 或 [Arch Linux 中文维基](https://wiki.archlinuxcn.org/wiki/Fcitx5) 折腾 Fcitx5 的配置喵～

## 常见问题

- 部分 Wayland 应用无法使用输入法
- ...