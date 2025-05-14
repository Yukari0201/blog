---
title: 本地浏览他人的 Hexo 博客
tags: 
  - blog
  - Hexo
categories: blog
date: 2025-05-14 17:40:33
---


## 注意事项

本教程只适用于 **博客作者上传了博客源码** 的情况，例如：[我的博客的源码](https://github.com/Yukari0201/yukari0201.github.io)

如果你已经会使用 Hexo 搭建博客，那么本教程对你可能没什么用（  
如果你不会使用 Hexo 搭建博客，读完本教程，或许可以帮助你学习 Hexo 的基本使用方法

## 前置条件

需要安装的软件：
- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/zh-cn)

### 写给 scoop 用户

```
scoop install git
```
```
scoop install nodejs-lts
```

## 让我们开始叭

### clone / 下载并解压 博客的源码

例如 clone 我的博客的源码
```
git clone https://github.com/Yukari0201/yukari0201.github.io.git
```

下载我的博客的源码：
```
https://github.com/Yukari0201/yukari0201.github.io/archive/refs/heads/hexo.zip
```

{% note warning %}

#### 注意

Hexo 博客源码的文件目录大致类似于下面所示
```
yukari0201.github.io/
├── scaffolds/
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source/
│   └── _posts/
│       └── xxx.md (博客的各文章)
├── themes/
│   └── .gitkeep
├── _config.next.yml
├── _config.yml
├── .gitignore
├── package.json
└── package-lock.json
```

如果你访问 Github 等源代码托管网站时看到的有很大差别，可能是因为：
- 博客作者并没有上传博客源码
- 博客作者将博客源码设置成另一分支，此时请切换分支查看

{% endnote %}

{% note default %}

#### 如果你的网络情况无法稳定连接 GitHub，可以试试镜像站或加速站

例如：
- [KGitHub](https://kkgithub.com/)
- [ghproxy](https://ghproxy.link/)
- [我基于 Cloudflare Workers 自建的 gh-proxy](https://ghproxy.yukari0201.ggff.net/) 
  - 详情请看我的另一篇拙作：[在 Cloudflare Workers 上部署 gh-proxy 以实现 GitHub 文件加速](../../2025-05-13/Deploying-gh-proxy-on-Cloudflare-Workers-for-GitHub-File-Acceleration)

加速站加速后 clone
```
git clone https://ghproxy.yukari0201.ggff.net/https://github.com/Yukari0201/yukari0201.github.io.git
```

加速站加速后 下载

```
https://ghproxy.yukari0201.ggff.net/https://github.com/Yukari0201/yukari0201.github.io/archive/refs/heads/hexo.zip
```

{% endnote %}

### 使用 npm 安装构建博客所需要的 modules

{% note warning %}

#### 注意

npm 默认的官方镜像源在国内的使用体验不佳，所以建议身处国内的用户修改为国内镜像源

```
npm config set registry https://registry.npmmirror.com
```

{% endnote %}

进入到你 clone / 解压 出来的博客源码目录，打开命令行运行：
```
npm install
```

等待跑完，这一步就算完成啦！

### 最后一步，本地浏览

```
npm run server
```
或者
```
npx hexo server
```

如果你用 npm 全局安装了 `hexo-cli`，也可以
```
hexo server
```

访问 http://localhost:4000/ 即可本地浏览博客

如果你看够了的话，`Ctrl`+`c` 快捷键即可退出
