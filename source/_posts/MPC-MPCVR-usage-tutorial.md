---
title: MPC-BE/HC + MPCVR 使用教程
date: 2025-01-05 20:16:45
tags:
- Windows
- DirectShow
- MPC-BE
- MPC-HC
- Media Player
---

## 观前声明

本人将主力播放器换成了 mpv 已经有很长一段时间了，所以本篇教程的更新或许不会那么及时。  
我的 mpv 自用配置：https://github.com/Yukari0201/mpv-config

本教程基于 Windows11 编写，兼容 Windows10 (x64)。  
32位 或 更低版本的 Windows 不保证兼容。

由于个人更喜欢使用 MPC-BE ，所以本教程更侧重于 MPC-BE + MPCVR，但也会给出 MPC-HC 的推荐设置。

由于我 [scoop](https://scoop.sh/) 用入魔了，所以增加了一些 scoop 相关的内容。**不明白请直接跳过**。

## 目录

- 兵欲善其事，必先利其器 -- 安装各播放器组件
  - 安装 MPC-BE + MPCVR
  - 安装 MPC-HC + MPCVR
  - 写给 scoop 用户：
    - 用 scoop 安装 MPC-BE + MPCVR
    - 用 scoop 安装 MPC-HC + MPCVR
- 简单调教 MPC-BE / MPC-HC
  - 简单调教 MPC-BE
    - 音频部分
    - 视频部分
    - 杂项
  - 简单调教 MPC-HC
    - 音频部分
    - 视频部分
    - 杂项
- MPCVR 推荐设置
- 完结撒花 ✿ヽ(°▽°)ノ✿
  - TODOs
  - 一些有用的教程指路

## 兵欲善其事，必先利其器——安装各播放器组件

MPC-BE 和 MPC-HC 根据个人喜好二选一即可。

### 安装 MPC-BE + MPCVR

#### 安装 MPC-BE

去 MPC-BE 的 [Github Releases](https://github.com/Aleksoid1978/MPC-BE/releases) 或 [Source Forge](https://sourceforge.net/projects/mpcbe/files/MPC-BE/Release%20builds/)  下载最新版本的安装包（名称类似 `MPC-BE.<版本号>.x64-installer.zip`），解压并运行安装程序  
安装程序有简体中文，大多数选项我相信各位都能看懂，所以我只提一点：  
在 `选择组件` 这一步请全部勾选，或者至少勾选 `MPC Video Renderer <版本号>`，这样就把 MPCVR 也顺带安装好了（同时请跳过本文的 `安装 MPC Video Renderer` 部分）。

![MPC-BE_Install_Select-Components](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_Install_Select-Components.png)

#### 安装 MPC Video Renderer

如果你在 MPC-BE 的安装过程中，`选择组件` 这一步勾选了 `MPC Video Renderer <版本号>`，那么请跳过此部分。

去 MPCVR 的 [Github Releases](https://github.com/Aleksoid1978/VideoRenderer/releases) 下载最新版本的 MPCVR（名称类似 ` MpcVideoRenderer-<版本号>.zip `），将其解压至一个你**不会去删除**的路径中，然后 点击 `Install_MPCVR_64.cmd` -> `鼠标右键`  -> `以管理员身份运行`。

### 安装 MPC-HC + MPCVR

#### 安装 MPC-HC

MPC-HC 的官方版本早已停更，现在是由 clsid2 进行维护。

去 MPC-HC 的 [Github Releases](hhttps://github.com/clsid2/mpc-hc/releases/latest) 下载最新版本的安装包（名称类似 `MPC-HC.<版本号>.x64.exe `），解压并运行安装程序  
安装程序有简体中文，大多数选项我相信各位都能看懂，所以我也是只提一点：
在 `选择组件` 这一步请保持默认选项（即勾选全部组件）。

![MPC-HC_Install_Select-Components.png](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-HC_Install_Select-Components.png)

#### 安装 MPC Video Renderer

MPC-HC 的默认安装选项已集成 MPCVR，无须另行安装。

### 写给 scoop 用户：

#### 用 scoop 安装 MPC-BE + MPCVR

```
scoop bucket add extras
scoop install mpc-be
```
```
scoop bucket add Yukari0201 https://github.com/Yukari0201/scoop-bucket
scoop install Yukari0201/mpcvr
```

#### 用 scoop 安装 MPC-HC + MPCVR

```
scoop bucket add extras
scoop install mpc-hc
```

便携版本的 MPC-HC 也已集成 MPCVR，无须另行安装。

## 简单调教 MPC-BE / MPC-HC

### 简单调教 MPC-BE

点击 `鼠标右键` -> `选项` 或 `查看` -> `选项` 进入设置

![MPC-BE_Settings](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_Settings.png)

Tips：更改完别忘了点击右下角的 `应用(A)` 哦~

#### 音频部分

大部分选项无须更改

`音频` -> `音频渲染器` -> `0. MPC Audio Renderer`(即默认选项)

![MPC-BE_Settings-Audio](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_Settings-Audio.png)

`音频` -> `声音处理` -> `声道合成` -> `混合声道至` -> `<根据你的设备更改>`(其中，`立体声` 即 `双声道`)  
注意：**不要**勾选 `要求解码器输出 2.0 立体声`

![MPC-BE_Settings-Audio-Processing](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_Settings-Audio-Processing.png)

`内置滤镜` -> `音频解码器` -> `音频解码器设置` -> `直通 (S/PDIF、HDMI)` -> 部分勾选 `你的设备支持的格式`  
注意：此部分选项只有拥有高端的音频设备(独立声卡/外置DAC)且需要直通某些格式的音频的用户才需要更改，一般用户无须更改

![MPC-BE_MPCAD](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_MPCAD.png)

#### 视频部分

`视频` -> `视频渲染器` -> 改为 `MPC 渲染器`  

`内置滤镜` -> `视频解码器` -> `视频解码器设置`

![MPC-BE_MPCVD](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_MPCVD.png)

- `格式转换` -> `RGB 输出级别` - 选 `PC (0-255)` (即默认值)
- `硬件加速` -> `首选解码器`
  - 如果你使用 MPCVR 或 madVR，保持默认的 `D3D11, DXVA2` 即可  
    - 选项的意思是，首先尝试使用 `D3D11 (Native)` 硬件解码，失败（例如其他不兼容 `D3D11 (Native)` 的视频渲染器，像是 `EVR`）则使用 `DXVA2 (Native)` 硬件解码  
  - Nvidia 显卡（除了 MX 系列）的用户也可以选择N卡专用的 `NVDEC (Nvidia only)`，可以多硬解一些格式  
  - Nvidia MX 系列显卡由于被老黄阉割了视频编解码单元，建议选择 `D3D11cb` 或 `D3D12cb`，并在 `显卡选择` 部分选择你的 `核显`  
    - `D3D12cb`(`D3D12 copy-back`) 比 `D3D11cb`(`D3D11 copy-back`) 更新，但在极端场景下才能感知到两者的性能差距。
  - **不推荐** 选择 `DXVA2`(`DXVA2 Native`)，它在部分情况下会出现画质损失

#### 杂项

- 记忆文件的播放位置 --- `播放器` -> `历史` -> `记住文件位置`
- 在进度条上显示章节标记 --- `播放器` -> `界面` -> `显示章节标记`
- 鼠标指向进度条时显示视频缩略图 --- `播放器` -> `界面` -> `搜索时显示预览`
- 开始播放后自动改变窗口大小 --- `播放器` -> `窗口尺寸` -> `开始播放后` -> `按照视频大小缩放` (建议 `100%`)
- 自动播放播放列表中的下一个视频 --- `回放` -> `打开设置` -> `额外添加到播放列表` (建议 `文件夹中的所有文件`)
- 更改字幕最大渲染分辨率(避免出现字幕很糊的情况) --- -> `字幕` -> `渲染` -> `纹理设置(......)` -> `最大纹理分辨率` (建议改为 `自身屏幕分辨率` / `1920x1080` 或许也已够用)

### 简单调教 MPC-HC

点击 `鼠标右键` -> `选项` 或 `查看` -> `选项` 进入设置

![MPC-HC_Settings](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-HC_Settings.png)

Tips：更改完别忘了点击右下角的 `应用(A)` 哦~

#### 音频部分

`回放` -> `输出` -> `音频渲染器` -> 选择 `MPC 音频渲染器`

MPC-HC 还有一个 `SaneAR 音频渲染器` 可用，但我不熟，所以暂时还是推荐使用和 MPC-BE 一样的 `MPC 音频渲染器`

![MPC-HC_Settings-Audio](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-HC_Settings-Audio.png)

`内部滤镜` -> `内部 LAV Filters 设置` -> `音频解码器`

`Mixing` 选项页：

![LAVAD_Mixing](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/LAVAD_Mixing.png)

- `Mixer` -> 勾选 `Enable Mixing`
- `Mixer` -> `Output Spesker Cofiguration` -> `<根据你的设备更改>`（其中 `Stereo` 即为 `双声道/立体声`）
- `Settings` -> `Don't mix Stereo sources`(双声道/立体声用户请勾选)
- `Settings` -> `Clipping Protectiom`(如果音频设备不是太差，建议取消勾选)

`Audio Settings` 选项页：  
注意：此部分选项只有拥有高端的音频设备(独立声卡/外置DAC)且需要直通某些格式的音频的用户才需要更改，一般用户无须更改

![LAVAD_Audio-Settings](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/LAVAD_Audio-Settings.png)

- `Bitstreaming(S/PDIF,HDMI)` -> `Formats` 勾选 `你的设备支持的格式`  
- 如果不清楚自己的设备支持的格式，可以在 `Bitstreaming(S/PDIF,HDMI)` -> `Options` -> 勾选 `Fallback to PCM if Bitstreaming is not supported`，该选项的意思是不支持直通的格式交给LAV解码。

#### 视频部分

`回放` -> `输出` -> `DirectShow 视频` -> 选择 `MPC 视频渲染器`

`内部滤镜` -> `内部 LAV Filters 设置` -> `视频解码器`

![LAVVD](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/LAVVD.png)

- `Hardware Acceleration` -> `Hardware Decoder to use:`
  - 如果你使用 MPCVR 或 madVR，请选择 `D3D11`，且不要在下方的 `Hardware Device to Use` 部分选择显卡，保持默认的 `Automatic(native)` 即可
  - Nvidia MX 系列显卡由于被老黄阉割了视频编解码单元，建议选择 `D3D11`，并在下方的 `Hardware Device to Use` 部分选择你的 `核显`
  - **不推荐** 选择 `DXVA2 (native)`，它在部分情况下会出现画质损失
- `Output Formats`
  - `RGB Output levels` -> 选择 `PC (0-255)`
  - `Dithering Mode` -> 抖动算法，看电影居多建议 `Oredered Dithering`，看动漫居多建议 `Random Dithering`
  - 实际上，在本篇教程的使用场景(渲染器选用 MPCVR)下，绝大多数情况下输出的都是和原片精度相同的YUV数据，`RGB Output levels` 和 `Dithering Mode` 的选项**绝大部分情况下**都不会生效

#### 杂项

- 记忆文件的播放位置 --- `播放器` -> `记忆文件播放位置`
- 鼠标指向进度条时显示视频缩略图 --- `调节` -> `在进度条显示视频预览`
- 开始播放后自动改变窗口大小 --- `回放` -> `缩放与对齐` -> `自动缩放` (默认已勾选；建议 100% [默认])
- 自动播放文件夹中的下一个视频 --- `回放` -> `回放结束后` (建议 `播放文件夹中的下一个文件`)
- 更改字幕最大渲染分辨率 (避免出现字幕很糊的情况) --- `字幕` -> `纹理设置（……)` -> `最大纹理分辨率` (建议改为 `自身屏幕分辨率` / `1920x1080` 也已够用)

LAV Filters 的三个组件都能显示托盘图标，在 `内部滤镜` -> `内部 LAV Filters 设置` -> `分离器`/`视频解码器`/`音频解码器` - 勾选左下角的 `Enable System Tray Icon` 即可  

![LAV_Enable-Sysytem-Tray-Icon](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/LAV_Enable-Sysytem-Tray-Icon.png)  

效果：  

![LAV_Tray-Icons](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/LAV_Tray-Icons.png)

## MPCVR 推荐设置

### 让 MPC-BE/HC 使用 MPCVR 作为视频渲染器

（如果你认真看完了 `简单调教 MPC-BE / MPC-HC` 部分，就会发现其实我们已经让播放器使用 MPCVR 作为视频渲染器了）  
但为了避免各位不小心忘记这一点（同时方便跳着看本文的童鞋），这里就再提一下。

#### MPC-BE 使用 MPCVR 作为视频渲染器

点击 `鼠标右键` -> `选项` 或 `查看` -> `选项` 进入设置  
`视频` -> `视频渲染器` -> 改为 `MPC 渲染器`

如果要进入 MPCVR 的设置，请点击右边的 `属性`

![MPC-BE_Settings_MPCVR](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-BE_Settings_MPCVR.png)

#### MPC-HC 使用 MPCVR 作为视频渲染器

点击 `鼠标右键` -> `选项` 或 `查看` -> `选项` 进入设置  
`回放` -> `输出` -> `DirectShow 视频` -> 选择 `MPC 视频渲染器`

如果要进入 MPCVR 的设置，请点击右边的 `设置`

![MPC-HC_Settings_MPCVR](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPC-HC_Settings_MPCVR.png)

### 调整 MPCVR 的设置

进入 MPCVR 的设置界面（方法在本文 `让 MPC-BE/HC 使用 MPCVR 作为视频渲染器` 部分已经提到过），你会看到下图的界面：

![MPCVR_default](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPCVR_default.png)

我不会班门弄斧地详细讲解各个选项的具体作用，如果需要了解，请看 MPC Video Renderer 的官方说明（内容是俄语，请善用翻译）：https://mpc-be.org/forum/index.php?topic=381

进入设置界面后，请根据下文文字内容自行更改（如果懒也可以直接抄下图内容，但我建议对各选项有一定了解后根据个人需要自行更改）

![MPCVR_custom](https://gcore.jsdelivr.net/gh/Yukari0201/Blog-CDN@main/images/MPC-MPCVR-usage-tutorial/MPCVR_custom.png)

- [左上] 勾选 `Use Direct3D 11` （Windows10/11 默认已勾选）
- [左上] `Texture format`(运算精度) - 更改为 `16-bit Floating Point`
  - 性能捉急可以选择 `10-bit Integer`，不建议选择 `8-bit Integer`
- [右上] `Show Statistics` 下方的 `Fixed font size` 请更改为 `Increase font by window`
  - 此选项是关于 MPCVR 的统计信息的（播放视频时通过 `Ctrl+j` 可以调出），更改此选项是为了避免出现统计信息的字体过小，不方便查看的问题。
- [右下] `Wait for V-Blank before Present` - 勾选可能会改善播放的流畅性
- `DXVA2 and D3D11 video processor` -> `Use for:` 全部取消勾选
  - `DXVA2 and D3D11 video processor` 会代替下文 `Shader video processor` 部分的设置，它的性能最好，但质量取决于显卡，并且可能受显卡驱动的影响导致颜色不准确（我就遇到过画面偏绿和画面偏灰暗的情况），非特殊情况**不建议**使用。

- `Shader video processor` 部分：
  - `Chroma scaling` - 建议 `Catmull-Rom`，性能捉急可以选择 `Bilinear`
    - 此选项选择的算法用于放大 yuv420/422 视频的色度（一般来说感知不是很明显）
  - `Upscaling` - 建议 `Jinc2m`
    - 此选项选择的算法用于放大视频画面（如 720p -> 1080p）
  - `Downscaling` - 建议 `Bicubic`/`Bicubic sharp`，后者比前者更锐利一点
    - 此选项选择的算法用于缩小视频画面（如 2160p -> 1080p）
  - `Use the "Upscaling" method to reducing the frame to 50%`
    - 此选项的意思为：目标尺寸≥源视频的50%时，使用与"Upscaling"相同的算法进行缩小视频画面。  
    是否勾选取决于你的个人喜好，我个人不勾选并在 `Downscaling` 部分使用 `Bicubic sharp` 算法。
  - `Use dithering`(使用抖动) - 强烈建议勾选

- `HDR` 部分  
这部分因为我没有可用的 HDR 显示器，暂时就不细讲了  
有这方面需求的用户请根据 MPCVR 官方说明进行更改
  - `Prefer Dolby Vision over PQ and HLG` 如果你需要观看 Dolby Vision 内容，请勾选
  - `Passthrough to display` - 如果显示器支持 HDR，请一定勾选
  - `Windows HDR` - 选择 `自动切换至 HDR 模式` 的方式，默认不自动切换
    - 如果显示器支持 HDR，请自行更改此选项
  - `If passthrough is impossible or disabled, then:` -> `Convert to SDR` - 如果显示器不支持 HDR，请勾选
    - 这将在 无法直通 HDR 数据给显示器时 或 不勾选 `Passthrough to display` 时 将 HDR 转换为 SDR

最后，别忘了点击右下角的 `应用(A)`，然后开启你的影音体验叭！

## 完结撒花 ✿ヽ(°▽°)ノ✿

### TODOs

- Nvidia RTX / Intel VSR 的使用教程DirectShow
  - 即 `DXVA2 and D3D11 video processor` -> 勾选 `Use for resizing` -> `Request Super Resolution` 部分

### 一些有用的教程指路

- [⚙️ 简易快速的mpcvr高画质播放方案指南](https://hooke007.github.io/DirectShow+/mpc.html) - 略有过时（MPCVR 更的太勤了）
- [基于 MPC-HC 和 madVR 的播放器配置入门](https://vcb-s.com/archives/16609)
- 萬年冷凍庫：
  - [系列之2─強大的外掛解碼方案-LAV Filters](https://lysandria1985.blogspot.com/2013/01/2-lav-filters.html)
  - [系列之3─最強渲染器-madVR](https://lysandria1985.blogspot.com/2013/01/3-madvr.html)
    - 知乎搬运（上篇）：https://zhuanlan.zhihu.com/p/73960527  
    - 知乎搬运（下篇）：https://zhuanlan.zhihu.com/p/73968849
- [Potplayer的合格安装与调校](https://github.com/hooke007/MPV_lazy/discussions/254) - LAV 以及 madVR 部分很值得参考
  - https://tieba.baidu.com/p/7171344019
