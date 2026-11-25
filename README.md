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

### 🚀 v8.2（最新 · versionCode 74）

- **署名区复核更新（2026-11-25）**：v7.7–v8.1 改动增量复核通过——累计 21 个 Kotlin 源文件、19 个矢量图标，依赖无新增，未发现复制或改编的第三方业务代码
- **四处署名文档同步**：THIRD_PARTY_NOTICES、APP 内开源许可页、README 中英；原创图标清单 10 → 12
- **校验通过**：编译成功、Lint 0 Error

### v8.1（versionCode 73）

- **统一返回导航**：所有二级页面（历史/日志/更新/清理/存储/许可/播放器）的返回按钮与系统手势统一回一级主面板，不再直接退出应用
- **保留主面板状态**：返回复用 MainActivity 实例，滚动位置、进度与统计状态不丢
- **仅顶层退出**：主页二级菜单先收起，仅顶层主面板执行退出；播放器保留锁屏/全屏的返回特例
- **校验通过**：编译成功、Lint 0 Error

### v8.0（versionCode 72）

- **紧急修复启动闪退**：v7.9 主页导航重构把两个面板直接挂到 ScrollView 导致启动崩溃，本次用单一容器包裹修复；v7.9 的 3 类二级菜单功能全部保留
- **校验通过**：编译成功、Lint 0 Error

### v7.9（versionCode 71）

- **主页导航重构**：9 个入口归为片段管理 / 偏好设置 / 关于与更新 3 类，首页只留 3 张分类卡，功能不减
- **页内二级菜单**：点分类卡原地切换，含返回栏与物理返回键处理
- **视觉与响应式**：分类卡渐变图标 + 条目预览 + 按压反馈，间距走设计令牌；560dp 居中兼顾桌面与移动端
- **校验通过**：编译成功、Lint 0 Error

### v7.8（versionCode 70）

- **片段重命名**：历史卡片与结果卡可改片段组名，保留 _partNNN 序号，相册/校验文件同步更新
- **命名模板**：支持 `{name}` / `{date}` 占位符与前后缀，可一键恢复默认
- **存储分析页**：片段按组聚合、按体积倒序展示占比，勾选批量释放空间
- **统计失败态修复**：片段统计异常时显示「点击重试」，不再伪装成空态
- **校验通过**：编译成功、Lint 0 Error

### v7.7（versionCode 69）

- **主页界面重新设计**：主题色渐变页头、带图标的渐变主按钮、本地片段概览卡，首页升级为有数据的内容页
- **统一设计语言**：间距/圆角/字号三套令牌 + 按压反馈，分区标题、2 列瓷片、清理横条、页脚隐私说明成套落地
- **二级页空态统一**：历史/日志/更新日志改为带图标 + 引导操作的空态组件
- **状态提示修复**：日志级别误判（"失败 0 个"不再误标失败）、通知权限拒绝弹窗说明 + 去设置入口
- **全项目功能体检**：16 项功能核实均有实现，输出缺口清单与 10 项分优先级建议
- **校验通过**：编译成功、Lint 0 Error

### v7.6（versionCode 68）

- **代码原创性核查（2026-11-22）**：逐文件复核 18 个 Kotlin 源码、17 个矢量图标、8 个形状/渐变资源与构建脚本，未发现复制或改编的第三方业务代码
- **非原创内容仅两类**：未修改的二进制依赖，以及 7 个 Material Icons 图标路径数据；两者此前均已署名，本次补齐细节
- **图标署名细化**：`ic_pause` 标注为等价重绘；Material 图标改为逐文件清单，其余 10 个图标明确为自绘
- **开发工具署名补齐**：Gradle、Kotlin 编译器、AGP / SDK Build-Tools、Pillow 补充来源、作者与许可
- **文档修正**：移除已不存在的 `progress_round.xml` 引用；APP 内署名页与仓库文档新增「代码原创性核查记录」，README 中英同步
- **无逻辑改动**，仅注释与署名文档；编译成功、Lint 0 Error

### v7.5（versionCode 67）

- **修复弹窗按钮被压成竖排**：三个按钮横排放不下时不再强行压缩子项，改为按自然宽度测量后整行纵向堆叠
- **按钮尺寸稳定**：单行 + 省略、最小高度 44dp、最小宽度 72dp
- **大屏/横屏一致**：弹窗宽度上限 420dp，平板、桌面与横屏下按钮不被拉成长条
- **删除按钮联动修复**：删除期间忽略播放完成与解码失败回调，避免自动续播重新占用待删片段
- **实测**：竖屏、横屏与 1.3 倍字号下的按钮与弹窗均无变形、裁切
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
- **Material Icons** — 7 个界面矢量图标的路径数据：`ic_arrow_back`、`ic_pause`（等价重绘）、`ic_play_arrow`、`ic_skip_next`、`ic_fullscreen`、`ic_fullscreen_exit`、`ic_video_placeholder`
  - 来源链接：https://fonts.google.com/icons
  - 出处说明：图标路径取自 Google Material Design Icons，用于 `app/src/main/res/drawable/` 下同名文件，各文件头已标注来源、出处、原作者与许可
  - 原作者署名：Google LLC
  - 许可：Apache License 2.0

上述组件均以**未修改**的二进制依赖或图标路径数据形式使用；启动图标、渐变与玻璃质感背景、其余 12 个界面图标为本项目原创绘制，未内置第三方字体、图片或音频素材。

2026-11-25 已完成增量复核（v7.7–v8.1 改动，累计 21 个 Kotlin 源码文件、19 个矢量图标）：未发现复制或改编的第三方业务代码，非原创内容仍仅为上述依赖与 7 个图标路径；历次核查范围、方法与结论见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) 第七节。

除上述第三方组件外，本项目的界面、业务逻辑、删除/预览/应用内更新等功能代码均为原创实现（AI 辅助生成并经维护者审阅）。

**许可声明**：本软件纯免费，仅供个人使用，不做任何商用。仓库当前未附带 `LICENSE` 文件，如需复用、修改或再分发代码，请先与维护者确认许可方式。

**生成声明**：纯AI生成。
