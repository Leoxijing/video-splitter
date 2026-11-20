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

### 🚀 v6.5 (latest · versionCode 57)

- **Frosted-glass floating menus**: home tiles and cards switch from translucent fills to real frosted glass — the page background is blurred and sampled aligned to each card's position, refreshing while scrolling, with a soft tint and highlight stroke
- **True dialog backdrop blur**: glass dialogs enable system-level FLAG_BLUR_BEHIND (API 31+), blurring the page behind them in real time; card fills are more translucent while text stays crisp
- **Theme color harmony**: custom-theme page gradients derive from the base hue at fixed lightness; the dark-mode primary button uses a mid-dark variant for clear white-on-color contrast (default theme unchanged)
- **Dark/light switch handling**: pages rebuild automatically on resume after the system dark/light mode changes in the background
- **Device-tested**: verified on Xiaomi 18 Pro Max (HyperOS 4.0 / Android 17) — install, launch, page navigation, dialogs, theme switching and dark/light toggling all pass with zero crashes or ANRs; feature logic unchanged

### v6.4 (versionCode 56)

- **Progress panel moved up**: the progress card now sits right below the primary CTA, with the tile grid after progress and results — split status is visible first
- **Tile icon redesign**: the stretched oval icon background becomes a fixed 46dp rounded square (15dp radius, squircle-style), soft and consistent
- **Unified spacing**: tile grid spacing follows the same rhythm as cards and buttons
- **Everything else unchanged**: progress card internals and data logic untouched, single-column layout kept, no tablet dual-pane

### v6.2 (versionCode 54)

- **Home information architecture rebuilt**: the title card and long button list become a hero headline + badge pill + large primary CTA + a 3-column icon tile grid; entries are scannable at a glance with balanced whitespace
- **Unified navigation**: the system action bar is removed; five secondary pages share one self-drawn top bar (circular back button + large title + subtitle); 8 original vector icons tinted by theme color
- **Component polish**: 24dp card radius with softer strokes, uniformly rounded thumbnails in the results area, dark-mode status bar/background auto adaptation
- **Everything else unchanged**: display/navigation only; split/pause/resume/export/logs/theme/update logic untouched, single-column layout kept, no tablet dual-pane

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
  - Provenance: invoked via the `ffmpeg-kit-min` variant of [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit) (see the dependency in `app/build.gradle.kts`); version bundled with `ffmpeg-kit-min:6.0-2` (FFmpeg 6.0 series)
  - Original author: The FFmpeg Team
  - License: upstream LGPL-2.1-or-later; built by ffmpeg-kit with `--enable-version3` and distributed as **LGPL-3.0**
- **ffmpeg-kit** — Android wrapper library for FFmpeg (`com.arthenica:ffmpeg-kit-min:6.0-2`)
  - Source: https://github.com/arthenica/ffmpeg-kit
  - Original author: Tanersener (Arthenica)
  - License: LGPL-3.0
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
