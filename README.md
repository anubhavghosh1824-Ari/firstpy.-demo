# 🏎️ 2D Top-Down Racing Game

A **production-quality, single-file** browser racing game built with vanilla JavaScript, HTML5 Canvas and CSS — no frameworks, no build step, no external dependencies.

## ▶️ Play Now

> **[🏁 Open the game](https://anubhavghosh1824-Ari.github.io/firstpy.-demo/)**
> *(GitHub Pages — live after merging to `main`)*

---

## 🎮 Controls

| Device | Steer left | Steer right | Accelerate | Brake |
|--------|-----------|------------|-----------|-------|
| **Keyboard** | ← / A | → / D | ↑ / W | ↓ / S |
| **Touch buttons** | ◀ | ▶ | ⬆ GAS | — |
| **Tilt (mobile)** | Tilt left | Tilt right | Auto | — |

Tap **📱 TILT MODE** (top-right) to switch between on-screen buttons and device-tilt steering.  
On iOS 13+ you will be prompted to grant motion-sensor permission.

---

## 🏁 Features

### Gameplay
- **3-2-1-GO! countdown** before each race — physics locked during countdown so all cars start fairly
- **2 AI opponent cars** that follow the track and race against you
  - 🟡 *Sunny* — moderate speed (1/3 around the track)
  - 🔵 *Flash* — higher speed (2/3 around the track)
- **Race position display** — P1 / P2 / P3 updated live in the HUD
- **Lap timing** — current lap time and personal best, formatted as `m:ss.tt`
- **Lap counter** — counts completed laps (counterclockwise direction)

### Physics
- Fixed 1/60 s timestep with render interpolation (smooth at any frame rate)
- Newtonian kinematics: engine power, mass, drag, transmission curve
- **Lateral velocity cancellation** → grippy on-rail handling
- **Drift mechanic** → impulse clamping lets the car slide when pushed hard
- Skid-mark ring buffer (pre-allocated `Float32Array` — zero GC pressure)

### Controls
- State Design Pattern: `TouchState`, `TiltState`, `KeyboardState`, `AIState` all share the same `BaseInputState` contract — the vehicle never knows *how* it is controlled
- IIR low-pass filter on tilt sensor data (configurable α = 0.1)
- iOS 13+ `DeviceOrientationEvent.requestPermission()` flow built in

### Track & Visuals
- Elliptical oval with red/white kerb stripes, yellow centre dashes, checkered start/finish line
- 4 orange cone obstacles with circle-collision physics
- Grass off-track with increased drag penalty

---

## 🗂️ File Structure

```
index.html   ← entire game (HTML + CSS + JS, ~1,770 lines, no deps)
README.md
.github/
  workflows/
    pages.yml  ← GitHub Pages auto-deploy on push to main
```

---

## 🚀 Deploy Your Own Copy

1. Fork this repository
2. Go to **Settings → Pages → Source** and select **GitHub Actions**
3. Merge (or push) to `main` — the workflow deploys automatically
4. Your game will be live at `https://<your-username>.github.io/<repo-name>/`

---

## 🛠️ Local Development

No build tools needed — just open `index.html` in any modern browser:

```bash
# Option 1 — file:// (works for keyboard controls)
open index.html

# Option 2 — local server (required for tilt/DeviceOrientation on HTTPS)
npx serve .
# then open http://localhost:3000
```

> **Note:** The Device Orientation API requires HTTPS in production.  
> Use a local HTTPS proxy (e.g. `npx local-ssl-proxy`) to test tilt on a real device.

