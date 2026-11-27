# 第三方组件与开源许可声明

本文件是 VideoSplitter（视频分割）APP 的第三方组件清单与许可声明，随 APP 分发并在应用内「更新日志 → 开源许可」中展示。

- 适用版本：v7.6（versionCode 68）及以后；更早版本自 v6.6 起适用（v6.6 将 ffmpeg-kit 依赖换为 16 KB 对齐的维护构建，见下）
- 核查方式：逐文件检查 `app/src` 代码与资源、`app/build.gradle.kts` 依赖声明，并用 Gradle `releaseRuntimeClasspath` 依赖树确认实际打包内容；v6.6 另逐库检查 APK 内 `.so` 的 ELF PT_LOAD 对齐与 ZIP 偏移
- 结论：本项目未包含整段复制或改编自第三方项目的业务代码；随 APK 分发的第三方内容均为**未修改的二进制依赖**与**7 个图标路径数据**（2026-11-25 复核，详见第七节）

## 一、随 APK 分发的第三方组件

| 组件 | 版本 | 来源 | 原作者 | 许可 | 在本项目中的用途 |
| --- | --- | --- | --- | --- | --- |
| FFmpeg（libavcodec / libavformat / libavutil / libswresample / libswscale 等） | 随 ffmpeg-kit-min 6.0.4 打包（FFmpeg 6.0 系列） | https://ffmpeg.org/ | FFmpeg Team | 上游为 LGPL-2.1-or-later；经 ffmpeg-kit 以 `--enable-version3` 构建，随包以 **LGPL-3.0** 分发 | 无损切割（`-c copy` 流复制）与转封装 |
| ffmpeg-kit（本版使用 `dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4`） | 6.0.4 | 维护分支 https://github.com/ffmpegkit-maintained/ffmpeg ；上游 https://github.com/arthenica/ffmpeg-kit | 维护分支维护者 Jokobee；上游原作者 Tanersener（Arthenica） | **LGPL-3.0** | FFmpeg 的 Android/JNI 封装与命令执行；上游 2025 年归档后由社区接续维护，保持 `com.arthenica.ffmpegkit` API 不变，并将原生库改为 16 KB 对齐 |
| libc++_shared.so（随上述 ffmpeg-kit 构建分发） | 随 Android NDK 版本 | https://github.com/llvm/llvm-project | LLVM Project / The Android Open Source Project | **Apache-2.0 WITH LLVM-exception** | C++ 标准运行库，ffmpeg-kit 原生库的运行依赖 |
| smart-exception-java / smart-exception-common（`com.arthenica:smart-exception-*:0.2.1`） | 0.2.1 | https://github.com/tanersener/smart-exception | Tanersener | **BSD-3-Clause** | ffmpeg-kit 的传递依赖（内部异常封装） |
| AndroidX / Jetpack：`androidx.core:core-ktx:1.13.1`、`androidx.core:core`、`androidx.annotation`、`androidx.collection`、`androidx.concurrent`、`androidx.interpolator`、`androidx.lifecycle`、`androidx.arch.core`、`androidx.profileinstaller`、`androidx.startup`、`androidx.tracing`、`androidx.versionedparcelable` 等 | 1.13.1 及其传递版本 | https://developer.android.com/jetpack/androidx | The Android Open Source Project / Google LLC | **Apache-2.0** | `FileProvider`（APK 安装授权）等基础组件 |
| Kotlin 标准库：`org.jetbrains.kotlin:kotlin-stdlib`、`kotlin-stdlib-common`、`org.jetbrains:annotations` | 1.9.24 / 13.0 | https://kotlinlang.org/ | JetBrains s.r.o. | **Apache-2.0** | Kotlin 运行时 |
| Guava listenablefuture（`com.google.guava:listenablefuture:1.0`） | 1.0 | https://github.com/google/guava | Google LLC | **Apache-2.0** | AndroidX 的传递依赖 |
| Material Icons（图标路径数据） | — | https://fonts.google.com/icons | Google LLC | **Apache-2.0** | 界面矢量图标：`ic_arrow_back`、`ic_pause`、`ic_play_arrow`、`ic_skip_next`、`ic_fullscreen`、`ic_fullscreen_exit`、`ic_video_placeholder` |

许可全文：

- LGPL-3.0：https://www.gnu.org/licenses/lgpl-3.0.html
- LGPL-2.1：https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html
- Apache-2.0：https://www.apache.org/licenses/LICENSE-2.0
- BSD-3-Clause：https://opensource.org/license/bsd-3-clause

## 二、LGPL-3.0 合规说明（FFmpeg / ffmpeg-kit）

1. **未修改**：本项目未修改 FFmpeg、ffmpeg-kit 及 smart-exception 的任何源码或二进制，仅通过公开 API 调用。
2. **可替换性**：FFmpeg 以动态库（`.so`）形式随 APK 打包，Java/Kotlin 层通过 ffmpeg-kit 的公开 JNI 接口调用。需要替换库的用户可自行获取对应 AAR 或从源码重新构建 APK；本项目不限制此类替换，也不使用阻止替换的技术措施。
3. **源码获取**：
   - ffmpeg-kit 上游：https://github.com/arthenica/ffmpeg-kit （含 `min` 变体的构建脚本，项目已于 2025 年归档）
   - ffmpeg-kit 本版维护分支：https://github.com/ffmpegkit-maintained/ffmpeg （含构建脚本与许可说明）
   - FFmpeg：https://ffmpeg.org/download.html 与 https://git.ffmpeg.org/ffmpeg.git
   - libc++：https://github.com/llvm/llvm-project （随 Android NDK 分发）
   - AAR 坐标：`dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4`（Maven Central）；v6.5 及更早为 `com.arthenica:ffmpeg-kit-min:6.0-2`
4. **许可文本**：LGPL-3.0 全文链接见上；如需离线副本，可从上述官方地址获取。libc++ 适用 Apache-2.0 WITH LLVM-exception（全文 https://www.apache.org/licenses/LICENSE-2.0 与 https://llvm.org/LICENSE.txt ）。
5. **无 GPL 组件**：使用的是 `min` 变体（不含 `-gpl` 后缀），未启用 `--enable-gpl`，不包含 GPL 授权的 FFmpeg 组件。
6. **16 KB 对齐**：v6.6 起，APK 内全部 arm64 原生库的 ELF PT_LOAD 段按 16 KB 对齐（`p_align=0x4000`），且未压缩 `.so` 在 APK 内的 ZIP 偏移对齐到 16 KB 边界，满足 Android 15+ 对 16 KB 页大小设备的要求。此前版本的 4 KB 对齐库仅能在 4 KB 页内核上加载。

## 三、图标与视觉资源

- 7 个界面矢量图标的路径数据来自 Google Material Icons（Apache-2.0），已在各 `ic_*.xml` 文件头注释中标注来源、原作者与许可，并在 README「第三方组件与署名」区块列出：
  `ic_arrow_back`、`ic_pause`（按同一造型等价重绘）、`ic_play_arrow`、`ic_skip_next`、`ic_fullscreen`、`ic_fullscreen_exit`、`ic_video_placeholder`。
- 启动图标（`ic_launcher_foreground.xml`、`ic_launcher_background.xml`、`ic_launcher_monochrome.xml`、`mipmap-anydpi-v26/ic_launcher*.xml`）、渐变与玻璃质感背景（`bg_gradient.xml`、`glass_btn.xml`、`glass_btn_primary.xml`、`glass_card.xml`、`glass_card_dark.xml` 及 night 变体）、其余 12 个界面图标（`ic_back`、`ic_changelog`、`ic_clean`、`ic_history`、`ic_limit`、`ic_logs`、`ic_theme`、`ic_update`、`ic_rename`、`ic_storage` 等）为本项目原创绘制，不含第三方素材。
- 未内置任何第三方字体文件；界面文字使用系统字体（`Typeface.DEFAULT` / `MONOSPACE`）。
- `design_icons.py` 为开发期图标预览脚本（依赖 Pillow），不随 APK 分发，不属于分发内容。

## 四、开发与构建工具（不随 APK 分发）

以下工具仅用于构建与开发，未以代码或资源形式打包进 APK：

| 工具 | 来源 | 原作者 | 许可 | 用途 |
| --- | --- | --- | --- | --- |
| Gradle | https://gradle.org/ | Gradle Inc. | Apache-2.0 | 构建 |
| Kotlin 编译器 / kotlin-gradle-plugin | https://kotlinlang.org/ | JetBrains s.r.o. | Apache-2.0 | 编译 Kotlin |
| Android Gradle Plugin / Android SDK Build-Tools | https://developer.android.com/studio | The Android Open Source Project / Google LLC | Apache-2.0（SDK 使用另受 Android SDK 条款约束） | 打包 APK |
| Pillow | https://python-pillow.org/ | Jeffrey A. Clark 等 | MIT-CMU（HPND） | 仅 `design_icons.py` 生成图标预览 |

## 五、项目自身版权与许可

- 业务代码（`app/src/main/java/com/tools/videosplit/*.kt`）、自绘资源与文档由本项目维护者编写；其中代码在 AI 辅助下生成并经维护者审阅。
- **当前状态**：仓库未附带 `LICENSE` 文件；README 仅声明「本软件纯免费，仅供个人使用，不做任何商用」，该表述是使用声明而非标准开源许可证。
- **待确认**：若希望他人可合法复用、修改或再分发本项目代码，需要明确选择一个许可证（如 MIT、Apache-2.0）或明确保留「All rights reserved」。在确认前，默认保留所有权利，仅授权个人非商业使用。

## 六、仍需确认的事项

1. 项目自身许可证尚未确定（无 `LICENSE` 文件），见第五节。
2. FFmpeg 精确版本号：`ffmpeg-kit-min:6.0.4` 对应 FFmpeg 6.0 系列；若需逐位精确（如 6.0.x），可在设备上执行 `ffmpeg -version` 或查阅 AAR 内版本字符串确认。
3. LGPL 合规是否需要额外提供源码离线包（当前提供上游链接与 Maven 坐标）。
4. 本项目源码目前未在 GitHub 公开（仓库仅含文档与版本信息），因此「可替换库」依赖用户自行从 Maven 获取 AAR 重建；如需更完整的合规体验，可考虑公开源码或提供未签名构建说明。
5. AI 生成代码的相似性：2026-11-22 已逐文件复核（方法见第七节），未发现整段复制或改写痕迹；后续若发现与某开源项目高度相似，按同一规则补充署名。

## 七、代码原创性核查记录

### 2026-11-22 全量核查

- 核查范围：`app/src/main/java` 全部 18 个 Kotlin 文件（约 6900 行）、`app/src/main/res` 下 17 个矢量图标与 8 个形状/渐变资源、`AndroidManifest.xml`、`app/build.gradle.kts` 与 `settings.gradle.kts`、`design_icons.py`
- 核查方法：
  1. 逐文件检索版权头、许可证标识、外部链接与常见复制痕迹（`TODO`、`StackOverflow`、博客来源等）
  2. 逐个比对矢量图标 `pathData` 与 Material Icons：7 个命中（已在文件头署名），10 个为自绘（圆弧/贝塞尔曲线 + 自有坐标系，非 24 网格填充路径）
  3. 以 `releaseRuntimeClasspath` 依赖树核对实际打包组件，确认与第一节清单一致，无未声明依赖
  4. 通读共享工具与自定义控件（`Ui`、`Theme`、`Dialogs`、`PlayerActivity` 手势/画面适配、`MediaFiles`、`StatusBarProgress`、`AppLog`），确认无整段复制或改写自外部项目
- 结论：未发现复制或改编的第三方业务代码；非原创内容仅为未修改的二进制依赖与 7 个图标路径数据，均已在第一节与 APP 内「开源许可与第三方署名」页署名
- 未随包分发任何第三方字体、图片、音频素材；`design_icons.py` 为开发期预览脚本，不进入 APK

### 2026-11-25 增量复核（v7.7–v8.1 改动）

- 复核范围：v7.7 主页改版至 v8.1 统一返回导航期间新增与改动的代码——新增 `Nav.kt`、`ClipRename.kt`、`SplitRecords.kt`（Kotlin 文件 18 → 21，合计约 8100 行）、新增自绘图标 `ic_rename.xml` 与 `ic_storage.xml`（矢量图标 17 → 19），以及 `Ui`/`MainActivity`/`PlayerActivity` 等 15 个文件的导航与界面重构
- 复核方法：检索全部源码中的版权头、许可证标识、外部链接与常见复制痕迹（`TODO`、`StackOverflow` 等）；核对 `app/build.gradle.kts` 依赖声明无新增（仍为 `ffmpeg-kit-min:6.0.4` + `androidx.core:core-ktx`）；逐个检查新增图标文件头的原创声明注释
- 结论：未发现复制或改编的第三方业务代码；新增图标均为项目自绘并在文件头注明；`ChangelogActivity` 新增 raw.githubusercontent.com 与 cdn.jsdelivr.net 两个在线更新日志拉取地址（仅网络请求目标，不分发第三方代码，无需署名）
