# video-splitter

「视频分割」APP 的更新发布仓库。

APP 内「检查更新」读取本仓库最新 Release 中的 `version.json`，发现新版本后下载对应 APK 并调起安装。

## 文件说明

- `version.json`：最新版本信息（versionCode / versionName / APK 下载地址 / 更新说明）
- Release Assets：每个版本的 APK 与该版本的 version.json

## 下载地址

- 版本信息：`https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## 更新日志

### 🚀 v3.3（最新 · versionCode 25）

- **结果区改版**：原视频与分割后片段**分区展示**（原视频区含缩略图、文件名、大小和删除按钮；片段区独立分组标题）
- **片段行增加视频缩略图**：每个片段显示首帧缩略图（后台加载、中心裁剪），点击整行即可预览
- 片段按序号排序展示

### v3.2（versionCode 24）

- **修复更新无法安装**：改用官方 PackageInstaller 安装会话（微信同款机制），直接拉起系统安装确认页——不再依赖"打开方式"选择器（旧方式在小米系统上弹出的候选列表里没有安装器，导致无法完成安装）；会话失败自动回退通用方式，安装结果写入运行日志

> 完整更新日记（v1.0 至今全部版本，含以上版本）见 [CHANGELOG.md](CHANGELOG.md)

## 第三方组件与署名

本 APP 的视频切割能力基于以下开源项目，在此致谢并署名声明：

- **FFmpeg**（通过 [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit) 调用，`ffmpeg-kit-min` 变体）— 提供无损视频切割（`-c copy` 流复制）核心能力，采用 LGPL-2.1-or-later 许可。项目地址：https://ffmpeg.org/

除上述第三方组件外，本项目的界面、业务逻辑、删除/预览/应用内更新等功能代码均为原创实现。

**许可声明**：本软件纯免费，仅供个人使用，不做任何商用。

**作者：超级小爱 · APP v3.3**
