# VideoSplitter

**English** | [简体中文](README.md)

<p align="center"><img src="docs/banner.png" alt="VideoSplitter" width="720"></p>

An Android app for when a single video over 4 GB hits cloud-transfer limits: it splits large videos into segments under a size limit — **losslessly** (ffmpeg stream copy) — so they upload and share smoothly. With in-app updates, thumbnail previews, and one-tap original-file cleanup.

[**⬇️ Download latest release**](https://github.com/Leoxijing/video-splitter/releases/latest) · Android 10+ · Free for personal use, no commercial use

## Features

- **Split by size limit**: default 3.8 GB per segment; segment duration is derived from the actual bitrate
- **Lossless cutting**: ffmpeg `-c copy` stream copy — no re-encoding, no quality loss
- **Automatic re-split**: 5% safety margin; oversized segments are re-cut with a shorter duration
- **Live progress**: percentage, segment counter, and export progress bar
- **Segment preview**: thumbnails grouped separately from the original video; tap a row to open the player (seek bar / ±10 s skip)
- **Original cleanup**: second-level page with thumbnails and checkboxes; deletes directly (including recycle-bin leftovers)
- **In-app update**: check → download → system install session for one-tap upgrade
- **Full changelog in-app**: an "Update Log" page renders the complete version history offline
- **Frosted-glass light-purple theme**

## Screenshots

<!-- Put APP screenshots into docs/screenshots/ and reference them here, e.g.:
![Main](docs/screenshots/main.png)
-->

> Contributions of APP screenshots (main / results / player) are welcome — drop them into `docs/screenshots/`.

## Changelog

### 🚀 v3.4 (latest · versionCode 26)

- **GitHub repo revamp**: bilingual README (zh/en, modeled after the Pulse project) with a project banner
- **Full changelog built into the APP**: new "Update Log" entry on the main screen, offline access to all versions since v1.0

### v3.3 (versionCode 25)

- **Result section redesign**: original video and segments are shown in separate sections (original section with thumbnail, name, size and delete button; segments under their own group header)
- **Thumbnails on segment rows**: first-frame thumbnail per segment (background loading, center-cropped); tap the whole row to preview
- Segments sorted by index

> Full history (all versions since v1.0) lives in [CHANGELOG.md](CHANGELOG.md), also viewable in-app via "Update Log".

## Files

- `version.json`: latest version info (versionCode / versionName / APK URL / release notes)
- Release Assets: APK and `version.json` for each release
- `CHANGELOG.md`: complete update diary
- `docs/`: banner and screenshots

## Download

- Version info: `https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## Third-party & authorship

This app's video-splitting capability is built on the following open-source project, gratefully acknowledged:

- **FFmpeg** (invoked via [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit), `ffmpeg-kit-min` variant) — provides the core lossless splitting (`-c copy` stream copy), licensed under LGPL-2.1-or-later. Project: https://ffmpeg.org/

Apart from the third-party component above, the UI, business logic, cleanup/preview/in-app-update features are original implementations.

**License**: Free for personal use only; no commercial use.

**Author: Super XiaoAi · APP v3.4**
