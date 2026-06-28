# NEURAL COURIER 3D

**NEURAL COURIER 3D** is a dependency-free WebGL browser game built with plain HTML, CSS, JavaScript, SVG HUD overlays, and raw WebGL primitives.

You play as a **human courier riding a hoverboard through a living AI city**. The city is losing memories, civic systems are corrupted, security drones are hostile, and the final viral boss — **Trend Hydra** — tries to turn the whole city into a copy-paste machine.

> Repository: `AASoftIR/neural-3d-game-js`  
> Author: **AASoftIR** / **@aasoftir**  
> Status: playable prototype  
> Stack: Vanilla JS + WebGL + SVG + CSS  
> Build step: none

---

## Live Demo

```txt
https://aasoftir.github.io/neural-3d-game-js/
```

---

## Screens / Concept

The game is designed around a modern theme instead of a classic spaceship shooter:

- AI city courier fantasy
- Humanoid hoverboard player
- Memory capsules
- Corrupted civic nodes
- Firewall obstacles
- Security drones
- Reality-patching ultimate ability
- Boss fight against the Trend Hydra

---

## Features

### Game Design

- 4 mission-based levels
- Real objective progression
- Collect, repair, survive, and boss-fight gameplay
- Combo scoring
- Shields and health
- Temporary upgrades
- Ultimate ability: **Reality Patch**
- Auto performance mode

### 3D / Rendering

- Raw WebGL renderer
- Custom shader pipeline
- 3D camera
- Perspective projection
- Procedural city buildings
- Primitive-based humanoid player
- Animated hoverboard
- Drones, capsules, nodes, bullets, firewalls, and boss modules
- SVG cockpit and HUD overlay

### Controls

| Action | Controls |
|---|---|
| Steer | Mouse, touch, `A/D`, or left/right arrows |
| Jump | `W` or up arrow |
| Crouch | `S` or down arrow |
| Shoot patch launcher | Hold mouse/touch, `Space`, `J`, or `K` |
| Dash | `Shift` |
| Reality Patch ultimate | `E` or `Q` when charge is full |
| Mute/unmute | `M` |
| Debug overlay | `F3` or backtick |
| Toggle quality | `L` |

---

## Levels

### Level 1 — Memory Market

Collect blue memory capsules before the city forgets them.

**Goal:** collect 12 memory capsules.

### Level 2 — Empathy District

Repair corrupted civic nodes with the patch launcher.

**Goal:** repair 8 green nodes.

### Level 3 — Firewall Festival

Survive the firewall parade and defeat hostile security drones.

**Goal:** defeat 24 drones/seekers.

### Level 4 — Trend Hydra

Fight the viral boss that tries to flatten the AI city into one boring trend.

**Goal:** defeat the Trend Hydra.

---

## Powerups

| Upgrade | Effect |
|---|---|
| Tri Patch | Fires extra side patches |
| Rail Patch | Stronger piercing shots |
| Memory Magnet | Pulls pickups toward the player |
| Helper Drone | Adds delayed support shots |
| Shield Prism | Restores shield |
| Charge Capsule | Charges Reality Patch faster |

---

## Technical Architecture

The whole game lives in `index.html`.

```txt
index.html
├── HTML structure
├── CSS visual system
├── SVG cockpit / HUD layer
└── JavaScript game engine
    ├── WebGL setup
    ├── Matrix math
    ├── Mesh generation
    ├── Game state
    ├── Level system
    ├── Collision system
    ├── Renderer
    ├── Input system
    ├── Sound system
    └── HUD/debug system
```

No external packages are required.

---

## Rendering Pipeline

The renderer uses:

- `canvas.getContext("webgl")`
- one vertex shader
- one fragment shader
- manually generated mesh buffers
- custom matrix functions
- perspective projection
- look-at camera
- fog tinting
- simple diffuse/rim lighting

The game does **not** use Three.js or any external WebGL engine. That keeps the repo small and easy to host, but it also means the engine code is intentionally custom and minimal.

---

## Meshes

The game currently uses procedural primitive meshes:

- cube
- pyramid
- octahedron

These are reused to build:

- the player body
- hoverboard
- buildings
- memory capsules
- drones
- corrupted nodes
- firewall obstacles
- boss body
- boss satellites
- particles and bullets

This keeps performance stable and avoids loading external assets.

---

## Performance Design

The game is designed to run on weaker laptops.

Important performance choices:

- no npm bundle
- no texture downloads
- no external assets
- no heavy DOM animation
- single WebGL canvas for 3D
- small SVG overlay only for HUD/cockpit effects
- auto-switch to low-quality rendering if FPS drops
- lower device-pixel-ratio in low quality mode
- particle count reduction in low quality mode

Manual quality toggle:

```txt
Press L
```

---

## Debugging

Press:

```txt
F3
```

or:

```txt
`
```

to show the debug overlay.

The overlay shows:

- FPS
- frame time
- quality mode
- level
- progress
- entity counts
- bullet count
- particle count
- heat
- charge
- shield
- active upgrades

---

## Known Technical Issues

### 1. WebGL availability

Some browsers or old GPUs may disable WebGL. The game checks for WebGL and displays a fallback message if unavailable.

### 2. Mobile browser performance

Mobile performance depends heavily on GPU and browser power-saving behavior. The game supports touch controls, but very weak devices may need low-quality mode.

### 3. Audio starts only after interaction

Browser security rules prevent audio from playing before user interaction. The sound engine initializes after clicking/touching/starting the game.

### 4. GitHub Pages caching

After pushing updates, GitHub Pages may show an older version for a short time. Hard-refresh the page or wait for deployment to finish.

### 5. Private license vs public repo

This repo uses a restrictive source-available license. People can view the code, but they are not granted open-source rights to reuse, redistribute, sublicense, sell, or create public derivatives.

If you want maximum privacy, keep the repository private. If you publish it with GitHub Pages, the deployed site is publicly reachable.

---

## Local Run

Clone the repo:

```bash
git clone https://github.com/AASoftIR/neural-3d-game-js.git
cd neural-3d-game-js
```

Open directly:

```bash
xdg-open index.html
```

or run a tiny local server:

```bash
python3 -m http.server 8080
```

Then open:

```txt
http://localhost:8080
```

---

## Deploy to GitHub Pages

This repo includes a GitHub Actions workflow:

```txt
.github/workflows/pages.yml
```

Recommended GitHub Pages setting:

1. Go to repository **Settings**
2. Go to **Pages**
3. Under **Build and deployment**
4. Set **Source** to **GitHub Actions**
5. Push to `main`

The workflow deploys the repository root as a static site.

---

## Recommended First Push

For an empty repository:

```bash
git clone https://github.com/AASoftIR/neural-3d-game-js.git
cd neural-3d-game-js

# Copy these project files into the repo folder, then:
git add .
git commit -m "Initial release: Neural Courier 3D"
git branch -M main
git push -u origin main
```

---

## Repository Structure

```txt
.
├── .github/
│   └── workflows/
│       └── pages.yml
├── .gitignore
├── .nojekyll
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── SECURITY.md
├── TECHNICAL_NOTES.md
└── index.html
```

---

## Roadmap

Possible future improvements:

- split JavaScript into modules
- add save slots
- add more levels
- add proper 3D models
- add boss attack patterns
- add accessibility options
- add settings screen
- add touch UI buttons
- add screenshots/GIFs to README
- add PWA support
- add automated linting

---

## License

This project is **not open source**.

It is released under a restrictive source-available license. See:

```txt
LICENSE
```

Short version:

- viewing the code is allowed
- playing the hosted game is allowed
- copying, redistribution, commercial use, public derivatives, and sublicensing are not allowed without written permission
