---
title: 在 Cloudflare Workers 上部署 gh-proxy 以实现 GitHub 文件加速
tags:
  - Cloudflare Workers
  - gh-proxy
  - GitHub
date: 2025-05-13 18:16:44
updated: 2025-05-14 17:11:01
---


## 前言

众所周知，[GitHub](https://github.com/) 在国内的访问速度属实一言难尽，而知名 GitHub 文件加速网站 [ghproxy](https://ghproxy.link/) 则天天被"Wall"，于是笔者就想着自建一个类似项目，供自己~~使用~~折腾

本人在 Cloudflare Workers 上部署的 GitHub 文件加速服务（欢迎各位适度使用）：  
https://ghproxy.yukari0201.ggff.net/

但是，授人以鱼不如授人以渔，与其交给各位一个**不稳定**的加速地址，不如教各位**自行部署**，于是此文应运而生

## 开始之前的准备

- 一个 Cloudflare 账户
- 一个可以托管在 Cloudflare 的域名（可选）

{% note warning %}

#### 注意

Cloudflare Workers 默认的 worker.dev 域名无法在国内正常访问，如果需要在国内使用，则**必须**绑定一个域名

{% endnote %}

## 部署

### 创建 Worker 项目

1、登录 [Cloudflare Dash](https://dash.cloudflare.com/)
- 登录后，点击右上角的 `+ 添加` -> `Workers`

2、开始创建 Worker
- 在跳转到的 `开始使用` 新界面，点击最下面的 `从 Hello World! 开始` -> `开始使用`

3、更改默认名称
- 接下来，在输入框中，将 Cloudflare 生成的默认名称修改为你喜欢的名称（例如：`ghproxy`），方便查看、管理

4、最后，点击右下的 `部署` 即可

### 替换 worker.js 的内容

1、进入代码编辑器
- `部署` 完成之后，在跳转到的新界面中点击 `编辑代码`
- 如果你不小心点错了，点成了 `继续处理项目`，不用担心，只需要点击右上的 <i class="fa-solid fa-code"></i>`编辑代码` 按钮即可

2、替换代码
- 将 `worker.js` 的内容替换为 [hunshcn/gh-proxy](https://github.com/hunshcn/gh-proxy) 项目提供的 `index.js` 的内容，该文件加速后的链接如下（选择其中一个即可）：
  - [个人自建 gh-proxy 加速连接](https://ghproxy.yukari0201.ggff.net/https://raw.githubusercontent.com/hunshcn/gh-proxy/refs/heads/master/index.js)
  - [JSDelivr 加速链接](https://gcore.jsdelivr.net/gh/hunshcn/gh-proxy@master/index.js)

3、确认无误后，点击右上的 `部署` 即可

### 为部署好的 Worker 绑定自己的域名（可选）

#### 为什么需要绑定自己的域名？
- Cloudflare Workers 默认的 worker.dev 域名在国内被污染，无法正常访问
- 默认的 worker.dev 域名过长，不方便使用

#### 操作步骤

1、将域名托管至 Cloudflare
- 若已有域名，需将 DNS 解析迁移到 Cloudflare
- 若无域名，可通过 Cloudflare 注册 一个新域名
- 具体操作方式各位还请自行搜索

2、进入 Workers 管理界面
- 点击侧边栏的 `计算 (Workers)` -> `Workers 和 Pages`
- 找到你之前创建好的 Worker，点击 `添加绑定`

3、添加自定义域名
- 在跳转到的新界面中点击 `域和路由` -> `添加` -> `自定义域`
- 在输入框中输入 `<前缀>.<你托管到 Cloudflare 的域名>`
  - 例如我托管到 Cloudflare 的域名是：`yukari0201.ggff.net`，我输入的域名前缀为，`ghproxy`
  - 最终的访问域名即为：`ghproxy.yukari0201.ggff.net`

4、验证
- 访问 `https://<前缀>.<你托管到 Cloudflare 的域名>/`，验证是否生效

## 参考链接

- https://github.com/hunshcn/gh-proxy
- https://hunsh.net/archives/23/
