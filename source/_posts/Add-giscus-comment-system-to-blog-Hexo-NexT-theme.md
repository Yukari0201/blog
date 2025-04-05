---
title: 为个人博客添加 Giscus 评论系统 (Hexo + NexT 主题)
tags: blog
categories: blog
date: 2025-04-05 15:27:36
updated: 2025-04-05 17:58:01
---


## 前言

本人最近将博客的评论系统由 [Utterances](https://utteranc.es) 迁到了 [Giscus](https://giscus.app)，故写此文，作为备忘，同时也是分享。

本文只会简单介绍 giscus 在 Hexo + NexT 主题下的配置，更多高级用法请各位参考官方文档：https://github.com/giscus/giscus/blob/main/ADVANCED-USAGE.md

## 让我们开始叭

### 为 Github 仓库安装 Giscus app

访问 https://github.com/apps/giscus ，将 giscus app 安装到你想要存储评论的仓库中

Giscus 是基于 GitHub Discussions API 的评论系统，所以别忘了 **为此仓库开启 [GitHub Discussions](https://docs.github.com/en/discussions)** 哦～



### 为 Hexo + NexT 博客安装 giscus

在你的博客目录下打开命令行，执行以下命令：
```
npm install hexo-next-giscus
```

然后，复制 [hexo-next-giscus](https://github.com/next-theme/hexo-next-giscus) 项目 Readme 中 `Configure` 部分的代码块到你的 `_config.next.yml` 中
```yaml
giscus:
  enable: false
  repo: # Github repository name
  repo_id: # Github repository id
  category: # Github discussion category
  category_id: # Github discussion category id
  # Available values: pathname | url | title | og:title
  mapping: pathname
  # Available values: 0 | 1
  reactions_enabled: 1
  # Available values: 0 | 1
  emit_metadata: 1
  # Available values: light | light_high_contrast | light_protanopia | light_tritanopia | dark | dark_high_contrast | dark_protanopia | dark_tritanopia | dark_dimmed | preferred_color_scheme | transparent_dark | noborder_light | noborder_dark | noborder_gray | cobalt | purple_dark
  theme: light
  # Available values: en | zh-CN
  lang: en
  # Place the comment box above the comments
  input_position: bottom
  # Load the comments lazily
  loading: lazy
```

并在 `_config.next.yml` 中 设置 `comments.active` 为 `giscus`
```yaml
# Multiple Comment System Support
comments:
  # Choose a comment system to be displayed by default.
  active: giscus
```

### 配置 Giscus

访问 https://giscus.app ，在 `仓库：` 部分输入 `<你的 Github 用户名>/<你存储评论的仓库名>`  
并在 `Discussion 分类` 部分选择一个 Discussion 分类（推荐 `Announcements` 分类，以确保新 discussion 只能由仓库维护者和 giscus 创建）  
提示：在 `主题` 部分可以选择评论系统的配色方案，对于 NexT 的深色主题，我推荐 `noborder_gray`

![giscus.app](giscus.app.png)

最后，下滑至 `启用 giscus` 部分，复制下表中提到的内容至 `_config.next.yml` 中  
| `启用 giscus` 中 `<script>` 的属性 | 对应在 `_config.next.yml` 中的配置项 | `_config.next.yml` 中的注释 |
| --- | --- | --- | 
| `data-repo` | `repo` | Github repository name |
| `data-repo-id` | `repo_id` | Github repository id |
| `data-category` | `category` | Github discussion category |
| `data-category-id` | `category_id` | Github discussion category id |
| `data-theme` | `theme` |  |

比如：我的 `_config.next.yml` 中 `giscus` 部分是这样：
```yaml
giscus:
  enable: true
  repo: Yukari0201/yukari0201.github.io # Github repository name
  repo_id: R_kgDOK3p0uA # Github repository id
  category: Announcements # Github discussion category
  category_id: DIC_kwDOK3p0uM4CjDgc # Github discussion category id
  # Available values: pathname | url | title | og:title
  mapping: pathname
  # Available values: 0 | 1
  reactions_enabled: 1
  # Available values: 0 | 1
  emit_metadata: 1
  # Available values: light | light_high_contrast | light_protanopia | light_tritanopia | dark | dark_high_contrast | dark_protanopia | dark_tritanopia | dark_dimmed | preferred_color_scheme | transparent_dark | noborder_light | noborder_dark | noborder_gray | cobalt | purple_dark
  theme: noborder_gray
  # Available values: en | zh-CN
  lang: zh-CN
  # Place the comment box above the comments
  input_position: bottom
  # Load the comments lazily
  loading: lazy
```

## 大功告成！

你可以运行如下命令来测试一下：

```
hexo clean
hexo server
```

点进文章界面，滑到最底下，应该就可以看到评论框了

确认无误后，即可部署了
- 对于一键部署的博客来说，只需要运行 `hexo generate -d` 即可
- 对于使用 GitHub Actions 来部署的博客来说（比如我的博客），只需要提交(commit)并推送(push)即可

## (补充) 从 Utterances/Gitalk 迁到 Giscus

请参考：https://docs.github.com/en/discussions/managing-discussions-for-your-community/moderating-discussions#converting-an-issue-to-a-discussion

将已有的 Issue 转换为 Discussion 即可，这样就可以继承已有的评论，实现几乎无缝迁移

## 碎碎念

你可以在 https://github.com/Yukari0201/yukari0201.github.io 看到我的博客的所有源代码，所以，放心评论叭

~~博客评论系统换了一套，结果还是没有人发评论（~~
