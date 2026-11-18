# VideoSplitter

**English** | [简体中文](README.md)

An Android app for when a single video over 4 GB hits cloud-transfer limits: it splits large videos into segments under a size limit — **losslessly** (ffmpeg stream copy) — so they upload and share smoothly. With in-app updates, thumbnail previews, and one-tap original-file cleanup.

[**⬇️ Download latest release**](https://github.com/Leoxijing/video-splitter/releases/latest) · **Requires: Android 13+** · Free for personal use, no commercial use

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

### 🚀 v4.3 (latest · versionCode 35)

- **Silent auto update check**: checks for the latest version every time the app opens (quietly in the background, no waiting dialog) and only prompts when a new version is found
- **Fixed floating dialog buttons**: buttons are now built into the glass card with matching background and opacity, with deterministic light/dark color selection

### v4.2 (versionCode 34)

- **Two-row player controls**: the seek bar now gets its own full-width row (fixes it being squeezed to zero width), maximizing the drag area
- Compact button row — the next button is no longer pushed off-screen

### v4.1 (versionCode 33)

- **Draggable playback seek bar**: auto-refresh pauses while dragging, tracks your finger live, and seeks precisely on release (fixes the snap-back issue)
- **Playback time display**: current time / total duration shown on both sides of the seek bar, synced live while dragging

### v4.0 (versionCode 32)

- **Modern update-check dialogs**: custom glass-card dialogs (rounded, theme-colored, light/dark adaptive) replace the stock legacy windows
- **Dark mode completed**: status bar, action bar and system dialogs now fully adapt to dark mode (system-level theme switching)

### v3.9 (versionCode 31)

- **Background splitting**: foreground service keeps splits running across app-switch/screen-off; live progress in the notification bar with a completion alert
- **Pause / cancel, disk space pre-check, adjustable size limit** (1G–50G custom)
- **Continuous playback** across segments; new **Split History** page; full **dark mode** support; APK trimmed to arm64-v8a only

### v3.8 (versionCode 30)

- **New hand-designed APP icon**: deep-purple gradient background with a white play button split by a bright cyan cut line (right half offset) — vector-drawn, crisp at any size
- Removed the top banner image from README

> Full history (all versions since v1.0) lives in [CHANGELOG.md](CHANGELOG.md), also viewable in-app via "Update Log".

## Files

- `version.json`: latest version info (versionCode / versionName / APK URL / release notes)
- Release Assets: APK and `version.json` for each release
- `CHANGELOG.md`: complete update diary
- `docs/`: screenshots

## Download

- Version info: `https://github.com/Leoxijing/video-splitter/releases/latest/download/version.json`

## Third-party & authorship

This app's video-splitting capability is built on the following open-source project, gratefully acknowledged:

- **FFmpeg** (invoked via [ffmpeg-kit](https://github.com/arthenica/ffmpeg-kit), `ffmpeg-kit-min` variant) — provides the core lossless splitting (`-c copy` stream copy), licensed under LGPL-2.1-or-later. Project: https://ffmpeg.org/

Apart from the third-party component above, the UI, business logic, cleanup/preview/in-app-update features are original implementations.

**License**: Free for personal use only; no commercial use.

**Author: Super XiaoAi · APP v3.4**
