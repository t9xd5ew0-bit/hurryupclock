# Shot Clock — Cue Sports Timer

A tableside shot clock for pool and cue sports, with configurable timing rules, audible warnings, extensions, and an installable offline-capable web app.

<p align="center">
  <a href="https://t9xd5ew0-bit.github.io/hurryupclock/"><strong>Open the live Shot Clock</strong></a>
</p>

> GitHub does not render interactive iframes in repository READMEs. Use the link above to open the live app; it is hosted by GitHub Pages.

## Features

- Four ready-to-use rule presets plus a configurable custom preset.
- Large countdown display with progress bar, warning state, and time-expired/foul state.
- Per-rack extension allowance and shot/rack counters.
- Synthesized warning sounds and expiration horn through the Web Audio API; no audio files are needed.
- Sound profiles, volume, pitch, beep length, warning window, and optional final-three-second urgency.
- Optional vibration on supported mobile browsers.
- Optional automatic start when advancing to the next shot.
- Wake Lock support where the browser provides it, to help keep the screen awake during play.
- Settings saved locally in the browser on the current device.
- PWA manifest and service worker for browser installation and offline use after the app has been loaded online.

## Use the Timer

1. Open the [live app](https://t9xd5ew0-bit.github.io/hurryupclock/).
2. Select a preset along the top, or open **Rules** to adjust the timing and audio behavior.
3. Press **Start** or tap the clock to begin or pause the countdown.
4. Press **EXT** when an extension is used. The remaining extension count is shown above the clock.
5. Press **Next Shot** after a shot. The timer resets for the next turn; it can start automatically if that option is enabled.
6. Press **New** to begin a rack and reset the shot and extension counters.

The first shot of each rack uses the configured break time. Later shots use the base shot time. At zero, the timer shows the time-expired foul state.

### Presets

| Preset | Shot time | Break time | Extension | Extensions per rack | Warning |
| --- | ---: | ---: | ---: | ---: | ---: |
| WPA 30s (+30s) | 30s | 30s | 30s | 1 | 5s |
| Matchroom 30s (60s Break) | 30s | 60s | 30s | 1 | 5s |
| 45s Standard (+45s) | 45s | 45s | 45s | 1 | 10s |
| League 60s (+30s) | 60s | 60s | 30s | 2 | 10s |

### Keyboard Shortcuts

| Key | Action |
| --- | --- |
| `Space` | Start or pause the clock |
| `E` | Use an extension |
| `N` or `Right Arrow` | Advance to the next shot |
| `R` | Start a new rack |
| `Escape` | Close the Rules dialog |

Shortcuts are ignored while typing in text or number fields.

## Install on a Device

The site is served over HTTPS, which is required for service workers and browser PWA installation.

- **Android / Chrome:** Open the browser menu and choose **Install app** or **Add to Home screen** when offered.
- **Desktop Chrome or Edge:** Use the browser's **Install** control or the install option in the browser menu.
- **iPhone / iPad:** In Safari, use **Share → Add to Home Screen**.

There is no in-app install button. Installation is provided by the browser. The exact menu wording and availability vary by browser and platform.

## Offline Use and Privacy

On first use, open the app while online so the service worker can install and cache the app shell. It caches the HTML entry point, manifest, and icons. Successfully loaded Tailwind CSS and Google Fonts resources are also cached by the service worker for later requests. Offline availability for those external resources depends on their having loaded successfully before going offline.

Timer preferences are stored in the browser's local storage on that device; they are not synchronized between browsers or devices. The app has no application server or account system. Styling and fonts are loaded from Tailwind's CDN and Google Fonts while online.

## GitHub Pages Deployment

The live site is deployed from the `main` branch by [`.github/workflows/pages.yml`](.github/workflows/pages.yml). Pushes to `main` deploy automatically; the workflow can also be started manually with `workflow_dispatch`.

The repository root is the Pages site root. Keep the entry point named `index.html` and keep the manifest, service worker, and icon files alongside it. App asset paths are relative so they work under the repository's project-site path.

## Development

This is a small static web app with its timer logic and UI in [`index.html`](index.html). PWA metadata and offline behavior are in [`manifest.json`](manifest.json) and [`sw.js`](sw.js); the install icons are `icon-192.png` and `icon-512.png`.

There is no build step, package manager, or automated test suite. For local PWA testing, serve the repository over `http://localhost` or another secure origin; service workers do not run from a `file://` URL. Check timer start/pause, preset changes, extensions, rack resets, warning/expiry behavior, settings persistence, installation availability, and offline launch after an online visit.

## Browser Requirements

Use a current browser with JavaScript enabled. Audio, vibration, and screen wake behavior depend on browser and device support; audio may require a user gesture before playback. PWA installation is available only in browsers that support web app installation.

## License

No license file is currently included in this repository.
