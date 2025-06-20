---
title: Gaussians Viewer
emoji: 📊
colorFrom: red
colorTo: green
sdk: static
pinned: false



---

Check out the configuration reference at https://huggingface.co/docs/hub/spaces-config-reference

# Gaussian Splatting Viewer (WebGL)

A real-time WebGL renderer for [3D Gaussian Splatting for Real-Time Radiance Field Rendering](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/), enabling photorealistic interactive 3D scenes in the browser using splats—anisotropic Gaussian blobs—as scene primitives.

👉 [Live Demo](https://huggingface.co/spaces/MarawanMogeb/gaussians-splat)

---

## ✨ What is Gaussian Splatting?

Gaussian Splatting is a fast, real-time rendering technique that represents a 3D scene using thousands to millions of translucent ellipsoids (3D Gaussians). Compared to traditional neural radiance field (NeRF) methods, this approach is significantly more efficient and better suited for real-time applications.

This implementation is a **client-side viewer** written in **JavaScript + WebGL**, capable of rendering `.splat` files generated from tools like the original [gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting).

---

## 🎮 Controls

### Keyboard

- **Movement:**
  - `←` / `→` – Strafe left/right
  - `↑` / `↓` – Move forward/back
  - `Space` – Jump

- **Camera:**
  - `A/D` – Turn left/right
  - `W/S` – Look up/down
  - `Q/E` – Roll counter/clockwise
  - `I/K` / `J/L` – Orbit camera

- **Shortcuts:**
  - `0–9` – Load predefined camera views
  - `-` / `+` – Cycle cameras
  - `P` – Reset camera animation

### Mouse / Trackpad

- **Click + Drag:** Orbit
- **Right-click + Drag:** Move
- **Scroll / Pinch:** Zoom / Move
- **Shift/Ctrl + Scroll:** Move/Strafe in direction

### Touch (Mobile)

- One finger drag – Orbit
- Two-finger pinch – Zoom
- Two-finger rotate – Camera rotation
- Two-finger pan – Move up/down and sideways

---

## 📁 File Support

- Drag and drop `.splat` files directly to load and render.
- `.ply` files generated from Gaussian Splatting pipelines will be auto-converted to `.splat`.
- Load camera paths with `cameras.json`.

---

## 🔧 Features

- ✔ Real-time rendering with WebGL 1.0
- ✔ CPU-based splat sorting via Web Worker
- ✔ Progressive loading for large models
- ✔ URL-based view sharing and camera saving
- ✔ Compact `.splat` format support

---

## ⚙ Technical Notes

- Uses **WebGL 1.0**, making it compatible with most browsers, including Safari and Firefox.
- Asynchronous **CPU-side sorting** ensures compatibility and responsiveness.
- No external JS libraries — pure JavaScript and GLSL.
- **Vertex shader** computes splat screen-space projection.
- **Fragment shader** handles per-pixel alpha-blended rendering.

---

## 📖 How It Works

Each 3D Gaussian (splat) is projected onto the screen and rendered as a shaded quad:
- **Vertex Shader**: Projects the position and orients the splat using its scale and rotation.
- **Fragment Shader**: Computes pixel opacity from the distance to the center of the Gaussian.

Sorting splats before rendering is crucial due to transparency blending:
- Implemented using a CPU **Painter’s Algorithm** via Web Worker.
- Experimental GPU sorting (bitonic/radix sort) was considered but left out for compatibility.

---

## 📦 Deployment

You can embed or host your own version:
```bash
git clone https://huggingface.co/spaces/MarawanMogeb/gaussians-splat
# Open index.html in a local server (or deploy to Hugging Face Spaces)
