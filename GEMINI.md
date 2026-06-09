use this for skills:

https://github.com/sickn33/antigravity-awesome-skills/tree/main

https://github.com/sickn33/antigravity-awesome-skills/blob/main/skills/game-development/SKILL.md

---

# 🇸🇪 Midsommer Madness Developer Guidelines for Gemini (Flutter Version)

Welcome! This file contains developer context, architecture notes, and guidelines for working on this project.

## 🛠️ Build and Automation Commands

Use the provided `Makefile` to run, build, and debug this application:

* **Local Web Development**: `make dev` or `make run` (serves files directly from the `assets/` directory)
* **Compile Android App**: `make build-apk` (runs `flutter build apk --debug`)
* **Deploy to Device/Emulator**: `make install-apk` (runs `flutter install`)
* **Clean Build Directories**: `make clean` (runs `flutter clean`)
* **Monitor Logs**: `make logcat` (runs `flutter logs`)

## 📂 Project Architecture

* **Web Assets**: The core game is implemented in vanilla HTML, JS, and CSS located inside the `assets/` directory:
  * [index.html](file:///home/xbill/midsommer-flutter/assets/index.html): Entry point and mobile-first touch UI canvas.
  * [game.js](file:///home/xbill/midsommer-flutter/assets/game.js): Gameplay loop (60Hz fixed timestep), rendering, physics, procedural Web Audio synthesizer, and touchscreen joystick input logic.
  * [index.css](file:///home/xbill/midsommer-flutter/assets/index.css): Styling, layout, animations, and retro colors.
* **Flutter Wrapper**: Located in the main project, wrapping the web files inside a full-screen, landscape-locked `WebViewWidget`:
  * [main.dart](file:///home/xbill/midsommer-flutter/lib/main.dart): Sets up fullscreen sticky immersive mode, configures the `WebViewController` with unrestricted JavaScript, enables Web Audio playback, and loads the game from Flutter assets.
  * [pubspec.yaml](file:///home/xbill/midsommer-flutter/pubspec.yaml): Registers dependencies like `webview_flutter` and configures the `assets/` directory.

## ⚠️ Key Instructions for Gemini / Antigravity

1. **Asset Modifications**: If you modify `game.js`, `index.html`, or `index.css` under the `assets/` directory, the changes will be automatically picked up on the next hot restart or Flutter build.
2. **Web Audio Compatibility**: The Android WebView requires user interaction to initialize the Web Audio API context. Ensure `AudioContext` resumes on first touch/click.
3. **Responsive Canvas**: Keep the target aspect ratio in mind when tweaking layouts. Touch controls should dynamically scale.
