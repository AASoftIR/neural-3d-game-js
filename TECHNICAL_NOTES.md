# Technical Notes

This document explains how **NEURAL COURIER 3D** works internally and what technical problems may appear when hosting or running it.

---

## 1. Why raw WebGL?

The game avoids Three.js and other libraries so it can run as a single static file.

Benefits:

- tiny repository
- no dependency install
- no build step
- easy GitHub Pages deploy
- easier to understand the complete pipeline

Tradeoffs:

- more manual math
- more verbose renderer code
- no advanced model loader
- no scene graph
- no texture/material system

---

## 2. Main Engine Loop

The game uses `requestAnimationFrame`.

Each frame:

```txt
loop()
├── calculate delta time
├── update player
├── update world movement
├── spawn entities
├── update bullets
├── update enemies
├── update particles
├── update level progress
├── render WebGL scene
├── render SVG HUD effects
└── update HTML HUD
```

The frame delta is clamped to avoid unstable physics after tab switching or lag spikes.

---

## 3. Coordinate System

Approximate world axes:

```txt
X = horizontal lane movement
Y = height
Z = forward distance into the AI city
```

The player stays near the camera and the city/entities move toward the player. This creates forward motion without requiring an infinite world.

---

## 4. Camera

The camera is a custom `lookAt` camera.

It follows the player slightly, giving a hoverboard-racing feel:

```txt
eye    = behind and above player
center = ahead into the city
up     = positive Y
```

---

## 5. Mesh System

The engine generates a few primitive meshes directly in JavaScript:

- cube
- pyramid
- octahedron

Each vertex contains:

```txt
position: x, y, z
normal:   nx, ny, nz
```

Those primitives are reused to make more complex shapes.

---

## 6. Shader

The game uses one vertex shader and one fragment shader.

Lighting is simple:

- diffuse light
- rim-like highlight
- fog mix by world depth
- pulse boost for hit/energy effects

This is not physically based rendering. It is intentionally stylized and fast.

---

## 7. Collision

Collision uses simple distance and bounding checks.

Examples:

- player vs pickup: distance near player body
- bullet vs enemy: Z proximity + X/Y distance
- player vs firewall: lane overlap + Z proximity + crouch/jump state
- enemy shot vs player: Z proximity + X/Y distance

This keeps gameplay responsive and cheap.

---

## 8. Performance Mode

The game tracks FPS. If FPS drops too much, it switches to low-quality mode.

Low-quality mode:

- lowers device pixel ratio
- reduces particle count
- keeps gameplay logic unchanged

Manual toggle:

```txt
L
```

---

## 9. Audio

The game uses Web Audio oscillator sounds.

There are no audio files. This avoids asset downloads.

Important browser behavior:

- audio cannot start until user interaction
- the audio context is created after click/touch/start
- muted mode can be toggled with `M`

---

## 10. SVG HUD

The cockpit and effects layer are SVG, separate from WebGL.

Why SVG?

- crisp HUD lines
- easy text-free cockpit effects
- cheap overlay effects
- keeps game objects in WebGL while UI remains flexible

---

## 11. GitHub Pages Notes

For static Pages deploy, this repo includes:

```txt
.github/workflows/pages.yml
.nojekyll
index.html
```

`.nojekyll` disables Jekyll processing. That is useful for pure static files.

---

## 12. Browser Compatibility

Recommended:

- Chrome / Chromium
- Edge
- Firefox
- recent Android Chrome

Possible problems:

- WebGL disabled by browser/GPU blocklist
- old Intel GPUs may have weak shader performance
- mobile browsers may reduce FPS in battery saver mode

---

## 13. Debug Checklist

If the game shows a black screen:

1. Open browser DevTools.
2. Check Console for WebGL errors.
3. Confirm WebGL is enabled.
4. Try pressing `L` for low-quality mode.
5. Test in Chrome/Chromium.
6. Serve with `python3 -m http.server 8080` instead of opening through unusual file managers.
7. Confirm `index.html` is at repo root for GitHub Pages.

---

## 14. Current Limitations

The game is intentionally still a prototype.

Known limitations:

- no external 3D model loading
- no saved settings
- no mobile on-screen buttons yet
- collision is arcade-style, not physics-engine-based
- all code is still inside `index.html`
- no automated test suite
- no accessibility settings yet

---

## 15. Suggested Refactor Later

A future cleaner version could split the file like this:

```txt
src/
├── main.js
├── engine/
│   ├── webgl.js
│   ├── matrix.js
│   ├── mesh.js
│   └── audio.js
├── game/
│   ├── state.js
│   ├── levels.js
│   ├── entities.js
│   ├── collision.js
│   └── input.js
└── ui/
    └── hud.js
```

For now, one file is easier to upload and run.
