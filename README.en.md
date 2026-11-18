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

### 🚀 v5.3 (latest · versionCode 45)

- **Long-press speed gesture**: long-press the video to enter speed control; keep holding and slide left/right to change speed in 0.1 steps (left lower, right higher, 0.5x ~ 3.0x)
- **Live feedback**: a centered overlay shows the current speed with one decimal and a 0.5~3.0 scale; playback follows the chosen speed instantly and keeps it after release

### v5.2 (versionCode 44)

- **Reliable splitting**: output names are auto-deduplicated (never overwrite previous results) plus resume support — after a cancel/interruption, "continue last time" keeps finished segments and picks up from the breakpoint
- **Player upgrades**: playback speed (0.5x ~ 3.0x), aspect-ratio modes (fit / stretch / crop), and screen-lock to prevent accidental touches
- **Management & verification**: multi-select batch delete in history; pause/cancel directly from the notification; per-segment SHA-256 checksums generated on export
- **Persistent logs**: runtime logs are saved on-device and survive app restarts

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

**Generation notice**: Purely AI-generated.
