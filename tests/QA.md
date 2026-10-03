# Gameplay verification — 2026-10-02

24 simulation tests and 19 headless Chromium browser integration checks passed on the final implementation. JavaScript syntax checks passed. The browser suite reported no JavaScript exceptions, asset-loading errors or shader-compilation errors.

## Simulation coverage

Deterministic 1,200-world generation; biome and radius variation; pause; all WASD directions; world-vertical rise/descent; simultaneous normalized movement; mouse-derived orientation; boost/brake; hold/release cloning; the 50-probe limit; companion following; active ship switching; high-speed swept collision; tangential orbit movement; 50-probe warp stress; navigation arrival and manual cancellation; hostile encounters; enemy spawn deduplication; railgun aiming/damage/cooldown and planet occlusion; homing and unguided missiles; companion combat; enemy attacks on leader and clones; consciousness transfer; simultaneous final-ship destruction.

## Browser coverage

Black name-entry screen; local asset loading; start flow and control overlay; pilot name and health HUD; third-person WebGL rendering; actual W+D+Space input; Escape pause; consecutive C holds; companion health bars; Tab ship switching; mouse input and capture; 1/2 weapon keypresses; F warp toggle; N/G navigation; reticle lock and railgun damage; missile effects and damage; the rendered 50-probe formation with over 40 visible companion health/name plates; destruction/transfer; complete fleet destruction and restart; viewport resizing; absence of browser and shader errors.

## Fixes verified

- Final-ship death during several enemy attacks now ends the game cleanly.
- Initial mouse capture no longer changes the starting view.
- Releasing C resets its hold latch immediately, even between frames.
- Weapon taps fire on keydown instead of depending on a held key spanning an animation frame.
- Companion formations stay ahead of the camera, avoiding probes passing directly through the third-person viewpoint.

## Test environment

Chromium 131 with software WebGL, driven by Playwright, at 1440×900 and resized to 1920×1080. Live input integration was checked in addition to deterministic simulation fixtures. Headless mouse capture produces paired synthetic deltas, so the mouse check verifies heading changes when those deltas arrive rather than requiring a nonzero final heading. All simulation and interaction checks completed successfully.

These tests cover the requested mechanics; they do not guarantee identical performance across every computer, browser, or graphics driver.

## Mobile update

The updated game passed 27 simulation tests, 19 desktop browser integration checks and 18 mobile browser checks (64 total). Three new simulation tests verify proportional analog speed, navigation cancellation and mixed keyboard/joystick speed limiting.

Mobile coverage includes automatic touch selection; touch guide and mouse-free startup; separate on-screen thumb regions; real simultaneous touchscreen input for movement and aiming; independent pointer release; immediate weapon taps; vertical movement; hold/release cloning; active-probe switching; warp/destination/navigation controls; simultaneous boost and movement; brake; swipe aiming; cancelled-touch cleanup; pause and input clearing; control-mode switching; landscape camera/layout adaptation; a 320px viewport without overlapping controls or horizontal overflow; and no JavaScript/shader errors.

Phone viewports tested in Chromium touchscreen emulation: 390×844 portrait, 844×390 landscape and 320×568 portrait. These checks exercise actual browser touch/pointer events through the input protocol, including distinct fingers; they are not physical iPhone or Android hardware tests. Portrait and landscape screenshots were reviewed. Names are kept on one line, HUD elements cannot expand the mobile viewport, and the mobile aiming label is shown above the reticle only when an enemy is locked.
