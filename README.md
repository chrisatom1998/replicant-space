# Replicant · Deep Space

A desktop and mobile single-player 3D browser game inspired by Dennis E. Taylor's Bobiverse. The player is a replicant controlling an original self-replicating probe. No official affiliation. No novel text or cover artwork is included.

## Play

Enter your name and press Start. The controls appear over the starting Earth scene. Press Begin flight to fly. Click the flight view to capture your mouse. Escape pauses and releases the mouse. In browsers that restrict mouse capture, moving the mouse over the flight view still turns the ship.

| Input | Action |
|---|---|
| Mouse | Turn and aim |
| W / S | Forward / reverse |
| A / D | Strafe |
| Space / Ctrl | Rise / descend in world coordinates |
| Shift | Boost |
| X | Brake |
| F | Toggle warp, with automatic near-planet safety slowdown |
| Hold C for 1.2 seconds | Create one clone; release before creating another |
| Tab | Switch the actively piloted ship |
| 1 | Launch a homing missile; target enemies in the reticle to lock |
| 2 | Fire railgun along ship's forward aiming direction |
| N | Cycle through nearby destination planets |
| G | Navigate to the selected world's safe orbital approach; movement cancels |
| Escape | Pause, release mouse, show controls |
| M | Toggle sound |

The fleet supports up to 50 living probes including the active ship. Autonomous probes follow in formation and fight nearby sentinels. Some planets have hostile defenders. Health bars appear above companion ships and in the HUD for the active probe. When the active probe is destroyed, control transfers to a surviving clone. Losing the entire fleet ends the run; Initialize again restarts it.

The universe contains 3,000 reproducible procedurally varied planets, including rocky, icy, ocean, volcanic and ringed gas worlds. The first scene shows Earth alone nearby. Flight is continuous between worlds, with floating-origin rendering and nearby-world culling with the 24 nearest worlds and selected destination visible at long range. Swept sphere collision detection and a surface safety shell protect both the leader and companions from entering planets. The universe is deliberately game-scaled rather than an astronomical simulation. HUD distances and speeds use consistent game-scale kilometers.

## Mobile mode

Touch controls are selected automatically on touch devices. You can also choose Touch before starting, or switch input modes from the pause screen.

- Left stick: proportional forward/reverse movement and strafing.
- Right stick: turn and aim; swiping empty space also turns the probe.
- Missile / Railgun: tap to fire immediately, or hold for repeated firing.
- Rise / Descend: hold to move vertically.
- Clone: hold for 1.2 seconds, release, then hold again for another companion.
- Boost / Brake: hold for stronger thrust or rapid stopping.
- Warp, Next world, Navigate and Switch: tap to toggle travel, select a destination, navigate, or change the active probe.
- Pause: stop the simulation and show the touch guide.

Movement, aiming and action buttons support simultaneous touches. Released or cancelled pointers reset their controls. The game works in portrait and landscape, with a wider view in landscape. Pixel density is reduced in touch mode to reduce graphics workload. No installation is needed.

## Run locally

All game assets are local; no build or runtime package installation is needed.

```sh
python3 -m http.server 8080 --directory dist
```

Open `http://localhost:8080` in a desktop browser with WebGL 2 and hardware acceleration. Serve over HTTP rather than opening the HTML as a file, because ES modules require an HTTP origin.

## Tests

```sh
npm test
npm run check
npm install
npx playwright install chromium
npm run test:browser
npm run test:mobile
```

The browser suite starts and closes its own temporary HTTP fixture server. It checks real keyboard/mouse handling, rendering, overlays, health bars, replication, combat effects, fleet switching, death/restart, resizing and browser/shader errors. `CHROMIUM_EXECUTABLE_PATH` can select another test browser. Software WebGL is enabled for headless test environments; the normal game uses the browser's graphics acceleration.

## Source

- `dist/sim.js`: deterministic universe, movement, fleet AI, combat and collision simulation.
- `dist/main.js`: Three.js rendering, camera, input, sound and HUD.
- `dist/touch.js`: multi-touch joysticks, aiming gestures and held action buttons.
- `dist/index.html` / `dist/style.css`: game screens and overlays.
- `tests/simulation.test.js`: 27 deterministic gameplay tests, including a 50-probe stress test.
- `tests/browser.test.cjs`: 20 desktop browser integration checks.
- `tests/mobile.test.cjs`: 18 touch browser checks in emulated phone viewports.

## Credits

Earth texture: NASA/Goddard Space Flight Center Scientific Visualization Studio. Blue Marble Next Generation data: Reto Stöckli (NASA/GSFC) and NASA's Earth Observatory. Source: https://svs.gsfc.nasa.gov/3615/ — `flat_earth03.jpg` is the equirectangular image supplied for wrapping onto a sphere.

Three.js r170: Copyright 2010–2024 Three.js Authors, MIT license. Bundled locally so the game does not depend on a third-party CDN at runtime. All probe geometry and procedural planet shaders are original for this game.
