# Blink3000 — Voluntary Blink Rate Tester

A Progressive Web App (PWA) that measures voluntary blink rate using your device's front camera and MediaPipe Face Mesh.

## Features

- **Three trial conditions**: Left eye only, Right eye only, Both eyes
- **Configurable duration**: 5s to 60s per trial (presets: 10, 15, 30, 60s, or custom)
- **Real-time blink detection** via Eye Aspect Ratio (EAR) on MediaPipe 478-landmark mesh
- **Live overlay**: EAR values displayed on each eye during tracking
- **Results**: Blinks/second (Hz) per trial condition
- **CSV export**: All blink timestamps (ms), trial metadata, and summary
- **PWA**: Installable, works offline after first load

## How to Deploy on GitHub Pages

1. Create a new GitHub repository (e.g. `blink3000`)
2. Upload all files in this folder to the repo root
3. Go to **Settings → Pages**
4. Set **Source** to `Deploy from a branch`, branch `main`, folder `/root`
5. Save — your app will be live at `https://<username>.github.io/blink3000/`

> **Important**: GitHub Pages requires HTTPS, which is necessary for camera access. ✓

## How It Works

1. Start camera — loads MediaPipe Face Mesh (refineLandmarks: true for iris/EAR accuracy)
2. Select your desired trial duration and which eye conditions to test
3. Press **⏺ RECORD** to start each trial
4. Blinks are detected when the Eye Aspect Ratio (EAR) drops below threshold (0.20)
5. Each blink event is timestamped in milliseconds
6. Trial ends automatically; results shown as blinks/second (Hz)
7. Export CSV with all raw events + summary

## CSV Format

```
session_id,trial,blink_n,timestamp_ms,elapsed_ms
1234567890,L,1,1234567891234,1023
...

# SUMMARY
trial,duration_s,blinks,blinks_per_s_hz
L,10.000,3,0.3000
R,10.000,4,0.4000
B,10.000,7,0.7000

# CONFIG
trial_duration_s,10
ear_blink_threshold,0.20
conditions_run,L+R+B
```

## Technical Notes

- EAR threshold: 0.20 (blink), 0.25 (re-open hysteresis)
- Camera: front-facing, 1280×720 @ 30fps (ideal)
- Model: MediaPipe FaceMesh via `@tensorflow-models/face-landmarks-detection@1.0.5`
- No data leaves the device — all processing is local

## Files

| File | Description |
|------|-------------|
| `index.html` | Main app (single-file) |
| `sw.js` | Service Worker for offline/PWA |
| `manifest.json` | PWA manifest |
| `icon-192.png` | App icon (192×192) |
| `icon-512.png` | App icon (512×512) |
