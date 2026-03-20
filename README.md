# Blinky 3000 — Voluntary Blink Rate Tester

A Progressive Web App (PWA) that measures voluntary blink rate using your device's front camera and MediaPipe Face Mesh.

## Features

- **Three trial conditions**: Left eye only, Right eye only, Both eyes
- **Configurable duration**: 5s to 60s per trial (presets: 10, 15, 30, 60s, or custom)
- **Real-time blink detection** via Eye Aspect Ratio (EAR) on MediaPipe 478-landmark mesh
- **Calibration** resting Open, Gentle Closed, threshold value calcualted.
- **Live overlay**: EAR values displayed on each eye during tracking
- **Results**: Blinks/second (Hz) per trial condition
- **CSV export**: All blink timestamps (ms), trial metadata, and summary
- **PWA**: Installable, works offline after first load


## How It Works

1. Start camera — loads MediaPipe Face Mesh (refineLandmarks: true for iris/EAR accuracy)
2. Select your desired trial duration and which eye conditions to test
3. Press Calibrate to start the Eye Open period, then the Gentle Closed period.
4. Press **⏺ RECORD** to start each trial
5. Blinks are detected when the Eye Aspect Ratio (EAR) drops below threshold (0.20)
6. Each blink event is timestamped in milliseconds
7. Trial ends automatically; results shown as blinks/second (Hz)
8. Export CSV with all raw events + summary


## Technical Notes

- EAR threshold: from calibration with re-open hysteresis
- Camera: front-facing, 1280×720 @ 30fps (ideal)
- Model: MediaPipe FaceMesh via `@tensorflow-models/face-landmarks-detection@1.0.5`
- No data leaves the device — all processing is local


|------|-------------|
| `index.html` | Main app (single-file) |
| `sw.js` | Service Worker for offline/PWA |
| `manifest.json` | PWA manifest |
| `icon-192.png` | App icon (192×192) |
| `icon-512.png` | App icon (512×512) |
