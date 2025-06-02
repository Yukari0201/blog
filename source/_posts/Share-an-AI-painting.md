---
title: 分享一幅 AI 绘画作品
date: 2025-06-02 19:32:51
tags:
  - AI
  - Stable Diffusion
---

## 前言

本人最近装上了 [Stable Diffusion Web UI (AUTOMATIC1111)](https://github.com/AUTOMATIC1111/stable-diffusion-webui)，尝试了一下 AI 绘图，并在 DeepSeek 的帮助下生成了一个勉强说得过去的图片，喜悦之余，分享一下

## 用到的参数、提示词等

### 模型

[Genshin_Kazuha_AP_v1](https://civitai.com/models/24973/genshinimpactkaedehara-kazuha)

### prompt

```
(solo:1.5), (1boy:1.6), masterpiece, best quality, highres, kaedehara kazuha, (official clothes:1.4), (silver-white hair:1.3), (long hair:1.2), (asymmetrical hairstyle:1.2), (distinctive red streak:1.4) on (left side:1.3), (red-tipped hair:1.2), (hair covering left eye:1.2), (small braid on left side:1.3) with (red strand:1.2), windswept hair, (anime hair:1.1), calm expression, wind element vision, anemo vision, maple leaf motif, wide sleeves, kimono-style top, hakama pants, shoulder armor, red rope belt, sake gourd at hip, katana (sword), standing, full body, intricate details, slim male body, flat chest, broad shoulders, handsome, anime style
```

### negative_prompt

```
(worst quality, low quality, normal quality:1.4), text, signature, username, watermark, artist name, error, cropped, jpeg artifacts, blurry, out of focus, extra limbs, disfigured, deformed, mutation, bad anatomy, bad proportions, malformed hands, fused fingers, too many fingers, long neck, extra arms, extra legs, extra feet, cloned face, missing arms, missing legs, three legs, three arms, four arms, four legs, two left hands, two right hands, multiple views, monochrome, grayscale, lowres, bad hands, bad fingers, missing fingers, fused fingers, poorly drawn hands, poorly drawn face, poorly drawn feet, poorly drawn eyes, poorly drawn eyebrows, poorly drawn nose, poorly drawn mouth, poorly drawn ears, poorly drawn hair, poorly drawn background,woman, female, girl, 1girl, 2girls, breasts, cleavage, curvy, feminine, female anatomy, makeup, lipstick, eyelashes, feminine pose, thighhighs, (solid red hair:1.2), (solid white hair:1.2), symmetrical hair, even hair color, hair not covering eye, (two braids:1.3), (no braid), (short hair), ponytail, twin tails, (hair over both eyes), (bangs covering both eyes), unnatural hair color, gradient hair
```

### sampler

`DPM++ 2M`

### cfgs

`10`

### steps

`50`

### width height

`768` `1024`

## 最终输出的图片

![img](00011-2355086137.png)

## 挖坑

或许我也可以写一篇 Stable Diffusion Web UI (AUTOMATIC1111) 的安装及使用教程？
