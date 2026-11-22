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
- **Full changelog in-app (online refresh)**: the "Update Log" page lists every version since v1.0, refreshes from the remote repository on open, and handles no-network, fetch-failure and empty states with retry
- **Batch sharing**: share all clips from the result card, or selected clips from history's manage mode, through the system share sheet
- **Split self-check**: segment durations are summed and compared with the source after each run; a mismatch is logged with a prompt to spot-check
- **Frosted-glass light-purple theme**

## Changelog

### 🚀 v7.6 (latest · versionCode 68)

- **Code originality review (2026-11-22)**: all 18 Kotlin sources, 17 vector icons, 8 shape/gradient resources and the build scripts were reviewed file by file; no copied or adapted third-party business code was found
- **Only two kinds of non-original content**: unmodified binary dependencies, and the path data of 7 Material Icons; both were already attributed and are now documented in more detail
- **Icon attribution refined**: `ic_pause` is marked as an equivalent redraw; the Material icons are listed file by file, and the other 10 icons are explicitly marked as original
- **Dev tool attribution completed**: Gradle, the Kotlin compiler, AGP / SDK Build-Tools and Pillow now list source, author and license
- **Doc fixes**: dropped the stale `progress_round.xml` reference; the in-app notices page and the repository notice gained a "code originality review" section, mirrored in both READMEs
- **No logic changes** — comments and attribution docs only; build succeeds, Lint 0 errors

### v7.5 (versionCode 67)

- **Dialog buttons no longer squeezed into vertical text**: when three buttons do not fit in one row, widths are measured first and the row falls back to a full-width vertical stack
- **Stable button sizing**: single line with ellipsis, 44dp minimum height, 72dp minimum width
- **Consistent on large screens and landscape**: dialog width is capped at 420dp
- **Delete-button fixes**: a deleting flag ignores completion/error callbacks so auto-advance cannot reopen the clip being removed
- **Tested**: portrait, landscape and 1.3× font scale all keep buttons and dialogs intact
- **Verified**: build succeeds, Lint 0 errors

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
- **Material Icons** — path data for 7 UI icons: `ic_arrow_back`, `ic_pause` (equivalent redraw), `ic_play_arrow`, `ic_skip_next`, `ic_fullscreen`, `ic_fullscreen_exit`, `ic_video_placeholder`
  - Source: https://fonts.google.com/icons
  - Provenance: icon paths from Google Material Design Icons, used in the same-named files under `app/src/main/res/drawable/`; each file header states source, provenance, author and license
  - Original author: Google LLC
  - License: Apache License 2.0

All components above are used as **unmodified** binary dependencies or icon path data. The launcher icon, gradient/frosted backgrounds and the other 10 UI icons are original artwork; no third-party fonts, images or audio are bundled.

A full review on 2026-11-22 of all 18 Kotlin sources and resources found no copied or adapted third-party business code; the only non-original content is the dependencies above plus those 7 icon paths. Scope, method and conclusion are documented in section 7 of [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

Apart from the third-party components above, the UI, business logic, cleanup/preview/in-app-update features are original implementations (AI-assisted, reviewed by the maintainer).

**License**: Free for personal use only; no commercial use. The repository currently ships no `LICENSE` file — please contact the maintainer before reusing, modifying or redistributing the code.

**Generation notice**: Purely AI-generated.
