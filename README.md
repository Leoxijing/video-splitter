# VideoSplitter 视频分割

[English](README.en.md) | **简体中文**

「视频分割」Android APP：单个视频超过 4G 时，云端传输往往受限——本工具按大小上限把大视频**无损**切成多段（ffmpeg 流复制），切完即可顺畅上传、分享。支持应用内更新、片段缩略图预览、原视频一键清理。

[**⬇️ 下载最新版本**](https://github.com/Leoxijing/video-splitter/releases/latest) · **系统要求：Android 13+** · 纯免费，仅供个人使用，不做商用

## 功能特性

- **按大小上限自动分段**：默认每段不超过 3.8G，按实际码率换算每段时长
- **无损切割**：ffmpeg `-c copy` 流复制，不重新编码、不损画质
- **超限自动重切**：带 5% 安全余量，切完发现某段仍超限自动缩短重切
- **实时进度**：百分比 + 已切片段数 + 导出进度条
- **片段预览**：结果区缩略图分区展示，点击整行进入播放器；双击播放/暂停、左右滑动快进快退、右下角全屏
- **原视频清理**：二级页缩略图勾选，直接删除（含回收站残留清理）
- **分割历史缩略图**：历史记录展示对应视频首帧，点击即可连续播放
- **应用内更新**：检查更新 → 下载 → 系统安装会话一键升级
- **完整更新日记**：APP 内置「更新日志」页，离线查看全部版本记录
- **磨砂玻璃浅紫主题**

## 更新日志

### 🚀 v5.1（最新 · versionCode 43）

- **稳定性修复**：日志页刷新不再拉回顶部并可自动跟随；缩略图解码器泄漏与线程阻塞修复；离开播放页清理手势状态
- **界面优化**：统一按压水波纹与卡片阴影；内容区宽度自适应并居中；主界面分组标题；历史页统计；日志页复制与自适应高度

### v5.0（versionCode 42）

- **滑动跟手优化**：横滑调进度时画面实时跳转、进度条与时间同步跟随；拖动定位合并节流，快速/反向/连续滑动不堆积延迟

> 完整更新日记（v1.0 至今全部版本）见 [CHANGELOG.md](CHANGELOG.md)；APP 内也可通过「更新日志」查看。

## 文件说明

- `version.json`：最新版本信息（versionCode / versionName / APK 下载地址 / 更新说明）
- Release Assets：每个版本的 APK 与该版本的 version.json
- `CHANGELOG.md`：完整更新日记

## 下载地址

- 版本信息：`https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## 第三方组件与署名

本 APP 在实现过程中使用或引用了以下第三方项目，在此明确标注来源链接、出处说明与原作者署名：

- **FFmpeg** — 提供无损视频切割（`-c copy` 流复制）核心能力
  - 来源链接：https://ffmpeg.org/
  - 出处说明：通过 [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit) 的 `ffmpeg-kit-min` 变体调用（依赖声明见 `app/build.gradle.kts`）
  - 原作者署名：FFmpeg 开发团队（FFmpeg Team）
  - 许可：LGPL-2.1-or-later
- **ffmpeg-kit** — FFmpeg 的 Android 封装库
  - 来源链接：https://github.com/arthenica/ffmpeg-kit
  - 原作者署名：Tanersener（Arthenica）
  - 许可：LGPL-3.0-or-later
- **Material Icons** — 播放、暂停、下一条、全屏、返回等界面矢量图标的路径数据
  - 来源链接：https://fonts.google.com/icons
  - 出处说明：图标路径取自 Google Material Design Icons，用于 `app/src/main/res/drawable/ic_*.xml`
  - 原作者署名：Google LLC
  - 许可：Apache License 2.0

除上述第三方组件外，本项目的界面、业务逻辑、删除/预览/应用内更新等功能代码均为原创实现。

**许可声明**：本软件纯免费，仅供个人使用，不做任何商用。

**生成声明**：纯AI生成。
