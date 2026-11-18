# VideoSplitter

**English** | [简体中文](README.md)

An Android app for when a single video over 4 GB hits cloud-transfer limits: it splits large videos into segments under a size limit — **losslessly** (ffmpeg stream copy) — so they upload and share smoothly. With in-app updates, thumbnail previews, and one-tap original-file cleanup.

[**⬇️ Download latest release**](https://github.com/Leoxijing/video-splitter/releases/latest) · **Requires: Android 13+** · Free for personal use, no commercial use

## Features

- **Split by size limit**: default 3.8 GB per segment; segment duration is derived from the actual bitrate
- **Lossless cutting**: ffmpeg `-c copy` stream copy — no re-encoding, no quality loss
- **Automatic re-split**: 5% safety margin; oversized segments are re-cut with a shorter duration
- **Live progress**: percentage, segment counter, and export progress bar
- **Segment preview**: thumbnails grouped separately from the original video; tap a row to open the player (double-tap play/pause, swipe to seek, fullscreen at bottom-right)
- **Original cleanup**: second-level page with thumbnails and checkboxes; deletes directly (including recycle-bin leftovers)
- **History thumbnails**: each split-history record shows the first frame of its video — tap to play all segments in sequence
- **In-app update**: check → download → system install session for one-tap upgrade
- **Full changelog in-app**: an "Update Log" page renders the complete version history offline
- **Frosted-glass light-purple theme**

## Changelog

### 🚀 v4.5 (latest · versionCode 37)

- **Bilibili-style player redesign**: immersive black UI with gradient top bar and bottom control area, icon buttons and larger touch targets
- **Double-tap to play/pause, swipe left/right to seek** (direction, distance and speed aware, with a centered live feedback overlay), **landscape fullscreen at bottom-right**, single tap to show/hide controls

### v4.4 (versionCode 36)

- **Thumbnails in Split History**: each record shows the first frame of its video on the left (loaded in the background, center-cropped, rounded corners)
- **Thumbnail fallback**: if the first segment fails to load, the next one is tried; if all fail, a placeholder icon is shown — records and continuous playback are unaffected

> Full history (all versions since v1.0) lives in [CHANGELOG.md](CHANGELOG.md), also viewable in-app via "Update Log".

## Files

- `version.json`: latest version info (versionCode / versionName / APK URL / release notes)
- Release Assets: APK and `version.json` for each release
- `CHANGELOG.md`: complete update diary

## Download

- Version info: `https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## Third-party components & attribution

This app uses or references the following third-party projects. Source links, provenance and original author attribution are stated explicitly below:

- **FFmpeg** — provides the core lossless video splitting (`-c copy` stream copy)
  - Source: https://ffmpeg.org/
  - Provenance: invoked via the `ffmpeg-kit-min` variant of [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit) (see the dependency in `app/build.gradle.kts`)
  - Original author: The FFmpeg Team
  - License: LGPL-2.1-or-later
- **ffmpeg-kit** — Android wrapper library for FFmpeg
  - Source: https://github.com/arthenica/ffmpeg-kit
  - Original author: Tanersener (Arthenica)
  - License: LGPL-3.0-or-later
- **Material Icons** — path data for the play, pause, next, fullscreen and back vector icons
  - Source: https://fonts.google.com/icons
  - Provenance: icon paths from Google Material Design Icons, used in `app/src/main/res/drawable/ic_*.xml`
  - Original author: Google LLC
  - License: Apache License 2.0

Apart from the third-party components above, the UI, business logic, cleanup/preview/in-app-update features are original implementations.

**License**: Free for personal use only; no commercial use.
