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
- **长按倍速播放**：长按画面立即以 2.0 倍临时播放，保持长按左右滑动按 0.1 调整（0.5~3.0 倍），松手恢复原倍速与原播放状态
- **原视频清理**：二级页缩略图勾选，直接删除（含回收站残留清理）
- **分割历史缩略图**：历史记录展示对应视频首帧，点击即可连续播放
- **应用内更新**：检查更新 → 下载 → 系统安装会话一键升级
- **完整更新日记**：APP 内置「更新日志」页，离线查看全部版本记录
- **磨砂玻璃浅紫主题**

## 更新日志

### 🚀 v5.5（最新 · versionCode 47）

- **长按即倍速播放**：长按画面立即以 2.0 倍临时播放（当前倍速更高则保持），长按期间左右滑动按 0.1 微调 0.5~3.0 倍
- **松手恢复**：松手立即回到原倍速与播放/暂停状态；暂停时长按会自动起播，松手回到暂停帧

### v5.4（versionCode 46）

- **署名与许可核查**：确认无整段复制的第三方代码；补全 smart-exception、AndroidX、Kotlin、Guava 的署名与许可，修正 FFmpeg 许可表述
- **许可文档**：新增 THIRD_PARTY_NOTICES.md，APP 内「更新日志 → 开源许可」可离线查看完整清单与 LGPL 合规说明

> 完整更新日记（v1.0 至今全部版本）见 [CHANGELOG.md](CHANGELOG.md)；APP 内也可通过「更新日志」查看。

## 文件说明

- `version.json`：最新版本信息（versionCode / versionName / APK 下载地址 / 更新说明）
- Release Assets：每个版本的 APK 与该版本的 version.json
- `CHANGELOG.md`：完整更新日记
- `THIRD_PARTY_NOTICES.md`：第三方组件清单、来源链接、原作者署名、许可证与 LGPL 合规说明

## 下载地址

- 版本信息：`https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## 第三方组件与署名

本 APP 在实现过程中使用或引用了以下第三方项目，在此明确标注来源链接、出处说明、原作者署名与许可。完整清单（含传递依赖、版本与 LGPL 合规说明）见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)，APP 内可在「更新日志 → 开源许可」离线查看。

- **FFmpeg** — 提供无损视频切割（`-c copy` 流复制）核心能力
  - 来源链接：https://ffmpeg.org/
  - 出处说明：通过 [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit) 的 `ffmpeg-kit-min` 变体调用（依赖声明见 `app/build.gradle.kts`）；版本随 `ffmpeg-kit-min:6.0-2` 打包（FFmpeg 6.0 系列）
  - 原作者署名：FFmpeg 开发团队（FFmpeg Team）
  - 许可：上游 LGPL-2.1-or-later；经 ffmpeg-kit 以 `--enable-version3` 构建，随包以 **LGPL-3.0** 分发
- **ffmpeg-kit** — FFmpeg 的 Android 封装库（`com.arthenica:ffmpeg-kit-min:6.0-2`）
  - 来源链接：https://github.com/arthenica/ffmpeg-kit
  - 原作者署名：Tanersener（Arthenica）
  - 许可：LGPL-3.0
- **smart-exception** — ffmpeg-kit 的传递依赖（`smart-exception-java` / `smart-exception-common:0.2.1`）
  - 来源链接：https://github.com/tanersener/smart-exception
  - 原作者署名：Tanersener
  - 许可：BSD-3-Clause
- **AndroidX / Jetpack** — `androidx.core:core-ktx:1.13.1` 及其传递依赖（core、annotation、collection、lifecycle、profileinstaller 等），用于 FileProvider 等基础组件
  - 来源链接：https://developer.android.com/jetpack/androidx
  - 原作者署名：The Android Open Source Project / Google LLC
  - 许可：Apache License 2.0
- **Kotlin 标准库** — `kotlin-stdlib:1.9.24`、`org.jetbrains:annotations:13.0`
  - 来源链接：https://kotlinlang.org/
  - 原作者署名：JetBrains s.r.o.
  - 许可：Apache License 2.0
- **Guava listenablefuture** — AndroidX 的传递依赖
  - 来源链接：https://github.com/google/guava
  - 原作者署名：Google LLC
  - 许可：Apache License 2.0
- **Material Icons** — 播放、暂停、下一条、全屏、返回等界面矢量图标的路径数据
  - 来源链接：https://fonts.google.com/icons
  - 出处说明：图标路径取自 Google Material Design Icons，用于 `app/src/main/res/drawable/ic_*.xml`，各文件头已标注来源、原作者与许可
  - 原作者署名：Google LLC
  - 许可：Apache License 2.0

上述组件均以**未修改**的二进制依赖或图标路径数据形式使用；启动图标、渐变与玻璃质感背景为本项目原创绘制，未内置第三方字体或素材。

除上述第三方组件外，本项目的界面、业务逻辑、删除/预览/应用内更新等功能代码均为原创实现（AI 辅助生成并经维护者审阅）。

**许可声明**：本软件纯免费，仅供个人使用，不做任何商用。仓库当前未附带 `LICENSE` 文件，如需复用、修改或再分发代码，请先与维护者确认许可方式。

**生成声明**：纯AI生成。
