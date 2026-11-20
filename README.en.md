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

### 🚀 v6.8 (latest · versionCode 60)

- **Download progress on the Super Island**: fixed the island not appearing for update downloads, or freezing at its first value. The download service never attached the island parameters (`miui.focus.param`) before — only the split notification did. The first notification now carries them, and every refresh rebuilds the notification and re-attaches the current progress
- **Throttled, accurate refresh**: progress updates use a double throttle — percentage change plus a 300 ms minimum interval — with 100% always flushed. Updates that are too dense get rate-limited by the system, which made the island stick at an old value. Without `Content-Length` the island shows an indeterminate "downloading" state
- **Changelog refreshed online**: the update-log page now shows a local first screen and refreshes from the remote repository, caching the full `CHANGELOG.md` and listing every version since v1.0; a status bar shows the current source and version count
- **States and fallback**: adding loading, no-network, fetch-failure and empty-remote states with a manual refresh entry; the remote is tried via raw link then CDN, and failures keep the local record visible
- **Full history restored**: `CHANGELOG.md` and the in-app copy are restored to the complete record since v1.0 (58 versions), readable offline; the README changelog still keeps only the latest two releases
- **Verified**: build succeeds, Lint 0 errors, `aapt dump badging` reports 60/6.8

### v6.7 (versionCode 59)

- **Resume fixed**: the resume offset now accumulates every kept segment's duration. It previously took only the last segment, so restarting after several segments re-cut content already produced, yielding overlapping clips
- **Integrity check**: after splitting, segment durations are summed and compared with the source (2% + 3 s tolerance); a mismatch is logged with a prompt to spot-check, and a passing run records segment count. Videos below the limit are counted as "skipped" instead of success
- **Result state fixed**: a run with failed segments no longer shows a check mark or a green "completed"; when every selected video is below the limit the app states there is nothing to split
- **Lifecycle and concurrency**: the main screen no longer rebuilds on rotation; UI updates go through a liveness check; the global statistics callback is unregistered when a task ends; notification pause/resume keeps the on-screen text in sync
- **Share closed loop**: the result card can share all clips at once, and history's manage mode can share selected clips through the system share sheet with multiple files
- **Storage and delete safety**: FileProvider is narrowed to the update package and export directory only; update packages live under `update/`; deleting the original is blocked while any clip failed to export; the cleanup page offers a tappable re-authorization entry when permission is missing

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
