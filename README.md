# VideoSplitter 视频分割

[English](README.en.md) | **简体中文**

「视频分割」Android APP：单个视频超过 4G 时，云端传输往往受限——本工具按大小上限把大视频**无损**切成多段（ffmpeg 流复制），切完即可顺畅上传、分享。支持应用内更新、片段缩略图预览、原视频一键清理。

[**⬇️ 下载最新版本**](https://github.com/Leoxijing/video-splitter/releases/latest) · **系统要求：Android 13+** · 纯免费，仅供个人使用，不做商用

## 功能特性

- **按大小上限自动分段**：默认每段不超过 3.8G，按实际码率换算每段时长
- **无损切割**：ffmpeg `-c copy` 流复制，不重新编码、不损画质
- **超限自动重切**：带 5% 安全余量，切完发现某段仍超限自动缩短重切
- **现代界面**：Hero 头部 + 图标瓷片导航的自绘界面，全局统一顶栏（圆形返回钮 + 大标题）、原创矢量图标随主题色着色，深色模式完整适配
- **实时进度**：阶段标签 + 大百分比 + 圆角渐变进度条与 0%/100% 刻度，随阶段配色并平滑过渡
- **主题色自由选**：8 种预设色板 + RGB 自定义滑条，主页/历史/删除/日志/播放器全页面同步换色
- **片段预览**：结果区缩略图分区展示，点击整行进入播放器；双击播放/暂停、左右滑动快进快退、右下角全屏
- **长按倍速播放**：长按画面立即以 2.0 倍临时播放，保持长按左右滑动按 0.1 调整（0.5~3.0 倍），松手恢复原倍速与原播放状态
- **原视频清理**：二级页缩略图勾选，直接删除（含回收站残留清理）
- **分割历史缩略图**：历史记录展示对应视频首帧，点击即可连续播放
- **应用内更新**：检查更新 → 下载 → 系统安装会话一键升级
- **应用日志**：统一字段（时间/类别/级别/来源/启动ID/记录ID/内容），卡片列表最新在前，支持按类别与失败筛选、导出、一键清空
- **完整更新日记（联网刷新）**：APP 内置「更新日志」页展示 v1.0 起全部版本，进入后自动联网获取最新记录，并补充无网络、获取失败、无数据状态与重试
- **批量分享**：结果页一键分享全部片段，历史页管理模式可分享选中片段，系统分享面板直接传出多个文件
- **分割自检**：每个视频切完累加各段时长与源视频比对，偏差超限写入应用日志并提示抽查
- **磨砂玻璃浅紫主题**

## 更新日志

### 🚀 v7.5（最新 · versionCode 67）

- **修复弹窗按钮被压成竖排**：三个按钮横排放不下时不再强行压缩子项，而是按自然宽度测量后自动改为整行纵向堆叠，文字不再竖排、点击区不再变形
- **按钮尺寸稳定**：统一单行 + 省略、最小高度 44dp、最小宽度 72dp，不同屏幕与系统字号下触控区域一致
- **大屏/横屏一致**：弹窗宽度上限 420dp，手机仍为 86%，平板、桌面与横屏下按钮不会被拉成长条
- **删除按钮联动修复**：删除期间忽略播放完成与解码失败回调，避免自动续播重新占用待删片段；删除前先暂停再停播，失败转系统确认时记录应用日志
- **实测**：竖屏三长按钮纵向堆叠、1.3 倍字号不裁切、两按钮弹窗保持横排；横屏播放页删除入口与两级确认弹窗正常，横屏 + 1.3 倍字号无溢出
- **校验通过**：编译成功、Lint 0 Error

### v7.4（versionCode 66）

- **清理页新增扫描已删除的分割片段**：连同系统回收站里的 `.trashed-` 残片一起扫描，以「已删除片段」单独列出；原视频已不在时也会列出，避免删除后仍占空间
- **片段清空后仍能找到原片**：新增分割来源记录，每次分割成功写入文件名与体积，不再只依赖残留片段名反推
- **扫描范围与排序**：原片优先，其次回收站残留，最后是已删除片段；同类按体积从大到小
- **删除加固**：统一走媒体库删除 + 路径兜底与重试，部分失败时明确提示「N 个未能删除」
- **实测**：MuMu 模拟器验证 5 类条目归类正确、删除后列表自动刷新、清理干净后正确显示空态
- **校验通过**：编译成功、Lint 0 Error

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
  - 出处说明：通过 ffmpeg-kit 的 `ffmpeg-kit-min` 变体调用（依赖声明见 `app/build.gradle.kts`）；版本随 `ffmpeg-kit-min:6.0.4` 打包（FFmpeg 6.0 系列）
  - 原作者署名：FFmpeg 开发团队（FFmpeg Team）
  - 许可：上游 LGPL-2.1-or-later；经 ffmpeg-kit 以 `--enable-version3` 构建，随包以 **LGPL-3.0** 分发
- **ffmpeg-kit** — FFmpeg 的 Android 封装库
  - 上游来源链接：https://github.com/arthenica/ffmpeg-kit ，原作者署名：Tanersener（Arthenica），许可：LGPL-3.0
  - 本版使用的构建：`dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4`（Maven Central），来源链接：https://github.com/ffmpegkit-maintained/ffmpeg ，出处说明：上游项目于 2025 年归档后由社区维护的接续分支，保持 `com.arthenica.ffmpegkit` API 不变；维护者：Jokobee，许可：LGPL-3.0
  - 更换原因：上游 6.0-2 的 arm64 原生库按 4 KB 对齐，不满足 Android 15+ 的 16 KB 页大小要求；6.0.4 的原生库全部按 16 KB 对齐
- **libc++_shared.so** — 随上述 ffmpeg-kit 构建分发的 C++ 标准运行库
  - 来源链接：https://github.com/llvm/llvm-project （随 Android NDK 分发）
  - 原作者署名：LLVM Project / The Android Open Source Project
  - 许可：Apache-2.0 WITH LLVM-exception
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
