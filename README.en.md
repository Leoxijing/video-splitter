# VideoSplitter

**English** | [简体中文](README.md)

An Android app for when a single video over 4 GB hits cloud-transfer limits: it splits large videos into segments under a size limit — **losslessly** (ffmpeg stream copy) — so they upload and share smoothly. With in-app updates, thumbnail previews, and one-tap original-file cleanup.

[**⬇️ Download latest release**](https://github.com/Leoxijing/video-splitter/releases/latest) · **Requires: Android 13+** · Free for personal use, no commercial use

## Features

- **Split by size limit**: default 3.8 GB per segment; segment duration is derived from the actual bitrate
- **Lossless cutting**: ffmpeg `-c copy` stream copy — no re-encoding, no quality loss
- **Automatic re-split**: 5% safety margin; oversized segments are re-cut with a shorter duration
- **Modern UI**: hero header with icon-tile navigation, a unified self-drawn top bar (circular back button + large title), original vector icons tinted by the user's theme color, full dark-mode support
- **Live progress**: phase badge, large percentage, rounded gradient bar with 0%/100% scale, phase-aware colors and smooth transitions
- **Theme color**: 8 preset palettes + RGB sliders, synced across home/history/cleanup/logs/player
- **Segment preview**: thumbnails grouped separately from the original video; tap a row to open the player (double-tap play/pause, swipe to seek, fullscreen at bottom-right)
- **Long-press speed playback**: hold the picture to play temporarily at 2.0x; keep holding and slide to fine-tune in 0.1 steps (0.5x~3.0x); release restores the previous speed and play state
- **Original cleanup**: second-level page with thumbnails and checkboxes; deletes directly (including recycle-bin leftovers)
- **History thumbnails**: each split-history record shows the first frame of its video — tap to play all segments in sequence
- **In-app update**: check → download → system install session for one-tap upgrade
- **App logs**: unified fields (time / category / level / source / launch ID / record ID / content), newest-first cards with category and failure filters, export and clear
- **Full changelog in-app**: an "Update Log" page renders the complete version history offline
- **Frosted-glass light-purple theme**

## Changelog

### 🚀 v6.6 (latest · versionCode 58)

- **Fixed the "Android app compatibility" dialog**: the system no longer shows "the following libraries are not 16 KB aligned" on launch. The previous ffmpeg wrapper shipped 9 arm64 native libraries aligned at 4 KB (`p_align=0x1000`); Android 15+ / HyperOS scans native libraries at install/launch and warns about unaligned ones
- **Scope**: the current device uses 4 KB pages, so the old libraries still load and the app always worked — the dialog is a forward-compatibility warning, not a crash. On devices with a 16 KB-page kernel, 4 KB-aligned libraries fail to load
- **Fix (API unchanged)**: the dependency is now `dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4`, a build with an **identical public API** (same FFmpeg 6.0 series / `min` variant / LGPL-3.0 / same transitive dependency; all 32 public classes compared signature-by-signature with no differences). All 10 arm64 native libraries have PT_LOAD segments aligned at 16 KB (`p_align=0x4000`), and uncompressed `.so` ZIP offsets are 16 KB aligned too
- **Zero business-code changes**: only the dependency coordinate and comments in `app/build.gradle.kts` changed; sources, resources and Manifest are untouched. Splitting, pause/resume, export, SHA-256, in-app update, theme, logs and notifications behave exactly as before
- **Verified**: build succeeds, Lint 0 errors, `aapt dump badging` reports 58/6.6, per-library ELF alignment and LOAD vaddr/offset congruence checks all pass; third-party sources, author attribution and licenses updated accordingly

### v6.5 (versionCode 57)

- **Frosted-glass floating menus**: home tiles and cards switch from translucent fills to real frosted glass — the page background is blurred and sampled aligned to each card's position, refreshing while scrolling, with a soft tint and highlight stroke
- **True dialog backdrop blur**: glass dialogs enable system-level FLAG_BLUR_BEHIND (API 31+), blurring the page behind them in real time; card fills are more translucent while text stays crisp
- **Theme color harmony**: custom-theme page gradients derive from the base hue at fixed lightness; the dark-mode primary button uses a mid-dark variant for clear white-on-color contrast (default theme unchanged)
- **Dark/light switch handling**: pages rebuild automatically on resume after the system dark/light mode changes in the background
- **Device-tested**: verified on Xiaomi 18 Pro Max (HyperOS 4.0 / Android 17) — install, launch, page navigation, dialogs, theme switching and dark/light toggling all pass with zero crashes or ANRs; feature logic unchanged

> Full history (all versions since v1.0) lives in [CHANGELOG.md](CHANGELOG.md), also viewable in-app via "Update Log".

## Files

- `version.json`: latest version info (versionCode / versionName / APK URL / release notes)
- Release Assets: APK and `version.json` for each release
- `CHANGELOG.md`: complete update diary
- `THIRD_PARTY_NOTICES.md`: third-party inventory with source links, author attribution, licenses and LGPL compliance notes

## Download

- Version info: `https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## Third-party components & attribution

This app uses or references the following third-party projects. Source links, provenance, original author attribution and licenses are stated explicitly below. The full inventory (including transitive dependencies, versions and LGPL compliance notes) lives in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and is also viewable offline in-app under "Update Log → Open-source licenses".

- **FFmpeg** — provides the core lossless video splitting (`-c copy` stream copy)
  - Source: https://ffmpeg.org/
  - Provenance: invoked via the `ffmpeg-kit-min` variant of ffmpeg-kit (see the dependency in `app/build.gradle.kts`); version bundled with `ffmpeg-kit-min:6.0.4` (FFmpeg 6.0 series)
  - Original author: The FFmpeg Team
  - License: upstream LGPL-2.1-or-later; built by ffmpeg-kit with `--enable-version3` and distributed as **LGPL-3.0**
- **ffmpeg-kit** — Android wrapper library for FFmpeg
  - Upstream source: https://github.com/arthenica/ffmpeg-kit ; original author: Tanersener (Arthenica); license: LGPL-3.0
  - Build used in this version: `dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4` (Maven Central), source: https://github.com/ffmpegkit-maintained/ffmpeg ; provenance: a community-maintained continuation after the upstream project was archived in 2025, keeping the `com.arthenica.ffmpegkit` API unchanged; maintainer: Jokobee; license: LGPL-3.0
  - Reason for the switch: the upstream 6.0-2 arm64 libraries are 4 KB aligned and do not meet the Android 15+ 16 KB page-size requirement; all libraries in 6.0.4 are 16 KB aligned
- **libc++_shared.so** — C++ standard runtime distributed with the ffmpeg-kit build above
  - Source: https://github.com/llvm/llvm-project (shipped with the Android NDK)
  - Original author: LLVM Project / The Android Open Source Project
  - License: Apache-2.0 WITH LLVM-exception
- **smart-exception** — transitive dependency of ffmpeg-kit (`smart-exception-java` / `smart-exception-common:0.2.1`)
  - Source: https://github.com/tanersener/smart-exception
  - Original author: Tanersener
  - License: BSD-3-Clause
- **AndroidX / Jetpack** — `androidx.core:core-ktx:1.13.1` and its transitive dependencies (core, annotation, collection, lifecycle, profileinstaller, etc.), used for FileProvider and other foundation components
  - Source: https://developer.android.com/jetpack/androidx
  - Original author: The Android Open Source Project / Google LLC
  - License: Apache License 2.0
- **Kotlin standard library** — `kotlin-stdlib:1.9.24`, `org.jetbrains:annotations:13.0`
  - Source: https://kotlinlang.org/
  - Original author: JetBrains s.r.o.
  - License: Apache License 2.0
- **Guava listenablefuture** — transitive dependency of AndroidX
  - Source: https://github.com/google/guava
  - Original author: Google LLC
  - License: Apache License 2.0
- **Material Icons** — path data for the play, pause, next, fullscreen and back vector icons
  - Source: https://fonts.google.com/icons
  - Provenance: icon paths from Google Material Design Icons, used in `app/src/main/res/drawable/ic_*.xml`; each file header states source, author and license
  - Original author: Google LLC
  - License: Apache License 2.0

All components above are used as **unmodified** binary dependencies or icon path data. The launcher icon and gradient/frosted backgrounds are original artwork; no third-party fonts or assets are bundled.

Apart from the third-party components above, the UI, business logic, cleanup/preview/in-app-update features are original implementations (AI-assisted, reviewed by the maintainer).

**License**: Free for personal use only; no commercial use. The repository currently ships no `LICENSE` file — please contact the maintainer before reusing, modifying or redistributing the code.

**Generation notice**: Purely AI-generated.
