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

### 🚀 v6.8（最新 · versionCode 60）

- **下载进度接入超级岛**：修复下载新版本时超级岛不显示、或进度停在首次数值的问题。根因是下载服务从未给通知附加超级岛参数，此前只有分割通知接入；现在首帧通知即带岛参数，并在每次刷新时重建通知、重新附加进度值
- **刷新节流与准确性**：进度刷新改为「百分比变化 + 最小 300ms 间隔」双重节流，100% 强制刷新；更新过密会被系统限流，反而让岛停在旧值。响应无 `Content-Length` 时以不确定进度显示「下载中」
- **更新日志联网刷新**：更新日志页升级为「本地首屏 + 联网刷新」，自动从远端仓库拉取完整 `CHANGELOG.md` 并写入本地缓存，展示 v1.0 起全部版本记录；顶部状态条显示当前来源与版本数量
- **状态与降级**：补充加载中、无网络、获取失败、远端无数据四类状态与手动刷新入口；远端按仓库直链 → CDN 回退，失败时保留本地记录
- **全量历史恢复**：`CHANGELOG.md` 与 APP 内置副本恢复为 v1.0 起完整记录（58 个版本），离线也能查看全部；README 更新日志区块仍只保留最新两版
- **校验通过**：编译成功、Lint 0 Error、aapt 版本号 60/6.8

### v6.7（versionCode 59）

- **断点续传修复**：续切起点改为累加所有已保留片段的时长；此前只取最后一段时长，完成多段后会从前几段末尾重切，产出内容重叠的片段
- **完整性自检**：每个视频切完累加各段时长与源视频比对（2% + 3 秒容差），偏差超限写入应用日志并提示抽查；未超上限的视频单独计为「跳过」，不再计入成功
- **结果状态修正**：有片段失败时不再显示对勾与绿色「已完成」；所选视频均未超上限时明确提示「无需分割」
- **生命周期与并发**：屏幕旋转不再重建主界面；界面更新统一经过存活检查；任务结束注销全局统计回调；通知栏「暂停/继续」同步界面文案
- **分享闭环**：结果页可一次分享全部片段，历史页管理模式可分享选中片段，系统分享面板直接传出多个文件
- **存储与删除安全**：FileProvider 收窄为仅更新包与导出目录；更新包统一存放到 `update/` 子目录；存在未导出片段时阻止删除原视频；清理页未授权时提供可点击的重新授权入口

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
