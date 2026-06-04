# A Night to Remember

A cinematic birthday experience web project.

## Project Structure

```
project/
├── index.html              — Main entry point
├── css/
│   ├── style.css           — Core visual system
│   └── effects.css         — Premium visual effects layer
├── js/
│   ├── core/
│   │   ├── config.js       — Master configuration (timing, easing, features)
│   │   ├── state.js        — Global reactive state store
│   │   └── app-controller.js — Master boot controller (loads last)
│   ├── engine/
│   │   ├── animation-engine.js   — GSAP animation system
│   │   ├── scene-manager.js      — Scene transition manager
│   │   └── interaction-engine.js — Micro-interactions & ripples
│   ├── systems/
│   │   ├── preloader.js          — Image preloader
│   │   ├── performance.js        — FPS monitoring & optimizations
│   │   └── three-background.js   — Three.js ambient background
│   └── main/
│       └── script.js       — Core scene engine & particle systems
└── assets/
    └── images/
        ├── img1.jpeg  — Photo grid image 1
        ├── img2.jpeg  — Photo grid image 2
        ├── img3.jpeg  — Photo grid image 3
        ├── img4.jpeg  — Photo grid image 4
        ├── msg1.jpg   — Message slide 1 image
        ├── msg2.jpg   — Message slide 2 image
        └── msg3.jpg   — Message slide 3 image
```

## Setup

1. Place your photos in `assets/images/` using the filenames above.
2. Open `index.html` in a browser — or better, serve via a local server:
   ```
   npx serve .
   # or
   python3 -m http.server 8080
   ```
3. To customize: edit the name "Nabila" in `index.html`, update slide messages, and replace images.

## Script Load Order (Critical)

1. GSAP (CDN)
2. Three.js (CDN)
3. `js/core/config.js` + `js/core/state.js`
4. `js/systems/preloader.js`
5. `js/main/script.js`
6. `js/engine/scene-manager.js`
7. `js/systems/three-background.js`
8. `js/engine/animation-engine.js`
9. `js/engine/interaction-engine.js`
10. `js/systems/performance.js`
11. `js/core/app-controller.js` ← boots last

## Bugs Fixed

- **bindIntroClick**: Replaced `cloneNode` with named handler pattern — prevents stale DOM references
- **initPhotogridNext / initMessageContinue**: Same fix — no more `cloneNode`
- **State references**: Fixed bare `State` calls in `preloader.js` to use `window.State`
- **Image paths**: Updated from `photos/` → `assets/images/`
- **Script order**: GSAP now loads BEFORE Three.js and before any module that needs it
- **THREE guard**: `createFloating` and `createBurst` return null gracefully if THREE is missing
- **Replay**: `scenes` array stays stable since we no longer clone DOM nodes
