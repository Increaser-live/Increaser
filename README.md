# The Increaser

**Download for Android:** [`apk/The-Increaser-0.3.0.apk`](apk/The-Increaser-0.3.0.apk) ·
**Play in the browser:** https://dawters-and-son.github.io/dawters-and-son/increaser/

*Every pass, a little more.* The DAWters and Son suite's live looper: six loop "cups", hands-free punch-in
with a count-in, start-on-sound and stop-when-you-stop triggers, gated takes, retakes, progressive build-up
recipes, Capture (keep the loop you just played), late-press grace, a big Fade out, live tempo moves (pitch
kept or tape), and optional USB / MIDI / game-pad pedals.
Free software under the GNU GPL v3 or later. Copyright (C) 2026 Josh Wilk.

- `python3 build.py` → `dist/increaser.html` (one self-contained page) and a web zip with a localhost launcher.
- `sh android/build-apk.sh` → `android/build/The-Increaser-<version>.apk` (WebView shell, `com.wilk.increaser`;
  needs `aapt apksigner zipalign dalvik-exchange libandroid-23-java` and a JDK). Saves go to Music/The Increaser.
  Without INCREASER_KEYSTORE / INCREASER_KS_PASS it is signed with a development key.
- The DAWters and Son website builds it and serves it at `/increaser/` (the suite's copy of this source lives in
  the [DAWters and Son repository](https://github.com/dawters-and-son/dawters-and-son) under `increaser/`).
- **Send to DAWters** (Export tab) opens the studio at `#receive` and posts a `dawters-send` message of
  `kind: 'stems'`; from a file it saves a `.dawsuite.json` for File → Import from the suite.

## Source

- `src/engine.js` — the looper engine (runs in the AudioWorklet and renders exports offline): loop grid,
  layers, punch jobs, sound trigger, silence stop, gates, WSOLA time-stretch, test band, click, limiter.
- `src/app.js` — the interface; `src/style.css` — the "Demitasse" design system; `src/index.html` — page shell.
- `src/fonts/` — Yesteryear, Oswald, Courier Prime (SIL OFL 1.1, see `src/fonts/OFL.txt`).

## Tests

- `node tools/test_engine.js` — engine checks (timing, pitch under tempo changes, layers, triggers, gates, Capture,
  grace, fades, CPU).
- `python3 tools/ui_check.py OUT`, `tools/ui_triggers.py OUT` and `tools/ui_live.py OUT` — headless Chromium walk-throughs
  with a fake microphone (needs Playwright); screenshots go to OUT.

## Installing the Android app

1. On the phone, open this page and download `apk/The-Increaser-0.3.0.apk` (tap the file, then **Download raw file**).
2. Open it. Android asks to allow installs from your browser or file manager: allow it for that app, then tap **Install**.
3. Allow the microphone when The Increaser asks. Saved recordings, stems and sessions go to **Music/The Increaser**.

Android 7 or newer. USB foot switches that type keys and game-pad pedals work through a USB-OTG adapter; MIDI
pedals don't yet (Android's WebView has no Web MIDI). This APK is signed with a development key: a later
release signed with the permanent key will ask you to uninstall this one first (save your sessions before).
