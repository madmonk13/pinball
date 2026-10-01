# Pinball Construction Kit 3D

A modern, browser-based take on Bill Budge's *Pinball Construction Set* (Electronic Arts, 1983). Build a pinball table from a box of parts, wire up its scoring, change the laws of physics, paint the playfield, and play it in real-time 3D.

Everything lives in a single file, `index.html`. It uses [Three.js](https://threejs.org/) from a CDN, and there is no build step.

## Quick start

Serve the folder with any static web server and open it in a modern browser (Chrome, Edge, Firefox or Safari):

```bash
python3 -m http.server 8765
```

Then visit <http://localhost:8765>.

Opening `index.html` directly from disk usually works too. A local server avoids browser restrictions on module scripts and images.

The first launch loads **Starlight**, a complete demo table. Press **Tab** to play it, then **1** to start a game.

## Modes

| Mode | What it's for |
|---|---|
| **✎ Build** | Top-down editor for placing, moving and configuring parts. |
| **🖌 Paint** | Paint art onto the playfield. Parts show as outlines while you paint. |
| **▶ Play** | Tilted 3D cabinet view with a score display. |

## Building a table

- Pick a part from the **parts box** on the left, then click the playfield to place it. Hold **⇧** to place several in a row.
- Drag a part to move it. The **inspector** on the right edits its position, rotation and properties.
- **Walls:** click to add points, then double-click or press **Enter** to finish. Click the first point to close a shape. On a selected wall, drag the square handles to reshape it, **Alt**-click a handle to delete it, or double-click a segment to add a point.

### Editor shortcuts

| Key | Action |
|---|---|
| Tab | Switch between build and play |
| V / W | Select tool / wall tool |
| Q / E | Rotate 15° (hold ⇧ for 1°) |
| Arrow keys | Nudge 0.05 (hold ⇧ for 0.5) |
| Ctrl/⌘ + D | Duplicate |
| Delete / Backspace | Delete |
| Ctrl/⌘ + Z, Ctrl/⌘ + ⇧ + Z | Undo / redo |
| Ctrl/⌘ + S | Save to library |
| G | Toggle grid snap |
| F | Fit the table in view |
| Mouse wheel | Zoom |
| Right-drag or Space-drag | Pan |

### Parts

| Part | Behaviour |
|---|---|
| Flipper (L/R) | Player-controlled. Length and colors are adjustable. Any number can be placed. |
| Plunger | Hold and release to launch. New balls are served here. |
| Pop bumper | Kicks the ball away on contact and scores. |
| Slingshot (L/R) | The inner face kicks the ball. |
| Kickout hole | Catches slow balls, scores, then ejects them along its arrow. |
| Magnet | Pulls the ball toward its centre. A negative strength repels. |
| Drop target | Drops when hit, and resets when its whole group is down. |
| Standup target | Lights when hit. |
| Rollover | Lights when the ball rolls over it. |
| Spinner | Spins when the ball passes through, scoring on each half turn. |
| One-way gate | Lets the ball pass only in the direction of its arrow. |
| Lamp insert | Decorative light (circle, arrow, triangle, star, square or pill) with an optional printed legend. It can be wired to game state. |
| Wall / Curved wall / Rubber band | Wood, plastic, metal or rubber, with different bounce for each. |
| Post | Rubber-ringed post. |

## Scoring and wiring (★ Rules)

- Every scoring part has **points**, plus a **bonus** value that builds the end-of-ball bonus.
- Drop targets, standups and rollovers belong to named **groups**. When every member is complete (all targets down, or all switches lit), the group pays its award and resets:
  - points only
  - advance the bonus multiplier (up to 5×)
  - extra ball
  - +10,000 bonus
- **Lane change:** groups with this option rotate their lit rollovers whenever a flipper is pressed.
- **Lamp modes:** always on, blink, chase, bonus multiplier ≥ level, shoot again, flash with bumpers, or a group's progress.
- **Game rules:** balls per game is configurable, and 1–4 players can play. The end-of-ball bonus is multiplied by the multiplier. Nudging too hard tilts the machine (after two warnings), which disables the flippers and forfeits the bonus. High scores are kept per table.

## Laws of physics (⚙ Physics)

Gravity, game speed, elasticity, kicker strength, flipper power and plunger power can all be adjusted live, even mid-game. Tilt can be turned off.

The simulation is a custom 2D solver on the playfield plane. It runs at a fixed 960 steps per second, with capsule collisions for walls and swept flipper contact, so fast balls don't tunnel through parts.

## Playing

| Key | Action |
|---|---|
| 1–4 | Start a game with that many players. Pressing 1 during ball 1 adds a player. |
| Left Shift / Z / ← | Left flippers |
| Right Shift / / / → | Right flippers |
| Space / Enter / ↓ | Hold to pull the plunger, release to launch |
| X / ↑ | Nudge |
| C | Cycle cameras |
| P | Pause |
| Esc | Back to the editor |

On touch screens, tap the left or right third of the screen for the flippers and hold the middle to plunge. Tapping also starts a game.

### Cameras

Choose a camera from the menu next to **Exit**, or press **C**. Your choice is remembered between sessions.

- **Cabinet** (the default): the whole table from the player's position. It refits automatically to any window shape and keeps the table below the score display.
- **Ball chase:** zooms in on the ball, looks ahead in the direction it's travelling, and leans toward the next flipper row below it. While the ball waits on the plunger, it frames the shooter lane instead.
- **Overhead** and **Low angle** views.

### Graphics quality

The **✦** menu in the top bar trades visuals for GPU load. The setting is remembered between sessions.

| Setting | Resolution | Shadows | Glow (bloom) | Accent lights |
|---|---|---|---|---|
| High | up to 2× | soft | on | on |
| Balanced | up to 1.5× | hard | on | on |
| Low | 1× | off | off | off |

## Painting (🖌 Paint)

The tools are brush, line, rectangle, ellipse, arrow, text (in several fonts), image stamp and eraser, with adjustable color, size and opacity. Paint is drawn on top of the theme's playfield color, pattern and image. It is saved with the table. Paint has its own undo, separate from the editor's.

## Themes (🎨 Theme)

Everything visual and audible can be themed:

- **Colors:** 32 settings, covering the backdrop, playfield, cabinet, rails, rubbers, every part type, the lights, the score display, and the app's own interface.
- **Materials and lighting:** ball shine, playfield gloss, glow strength, bloom, reflections, exposure, ambient and accent lights, and backdrop brightness.
- **Playfield:** a procedural pattern (rays, grid, checker, stars, wood, circles, diamonds or stripes) or your own image.
- **Images:** a backdrop behind the cabinet and backglass art on the backbox. Upload a file or use a URL; URLs must allow cross-origin use.
- **Score display:** dot matrix, vacuum fluorescent, LCD or marquee.
- **Sound set:** electro-mechanical chimes, arcade, synthwave, 8-bit chiptune or soft. All sounds are synthesized live with WebAudio, so there are no audio files.

Built-in presets: Classic '83, Neon Noir, Walnut & Brass, Deep Space, Retro 8-Bit and Sunset Arcade.

Themes can be saved to a library in the browser, or exported and imported as `.theme.json` files. A table always carries its own theme.

## Saving and sharing

- The current table is **autosaved** in the browser and restored on reload.
- **Save** adds it to your library in browser storage, and **Open** lists the library.
- **Export** downloads a `.pck3d.json` file containing the parts, rules, physics, theme and paint. **Import** accepts either a table or a theme file.

Browser storage is limited, typically to a few MB. Large uploaded images can exceed it. If they do, the app warns you, and Export is the reliable way to keep the table.

### Table file format

```jsonc
{
  "version": 1,
  "name": "Starlight",
  "physics": { "gravity": 1, "speed": 1, "elasticity": 1, "kick": 1, "flipper": 1, "plunger": 1, "tilt": true },
  "rules": { "balls": 3, "groups": { "lanes": { "points": 5000, "action": "multiplier", "laneChange": true } } },
  "parts": [ { "id": "…", "type": "bumper", "x": -3.55, "y": 29.5, "rot": 0, "radius": 0.95, "points": 100 } ],
  "paint": "data:image/png;base64,…",
  "theme": { "name": "Classic '83", "colors": { … }, "mat": { … }, "pattern": "rays", "images": { … }, "hud": "dmd", "sound": { … } }
}
```

Coordinates are in table units of roughly one inch. The playfield runs from x = −10.1 to 10.1 and y = 0 at the drain to about 42 at the top arch. Rotation is in degrees, counter-clockwise.

## Project layout

```
index.html           the whole app: UI, renderer, physics, editor, painter, themes, sound, game rules
.claude/launch.json  dev-server config for the Claude Code preview pane
```

Inside `index.html`, the script is organised into labelled sections: utilities, themes, sound, part definitions, renderer, part builders (`BUILD`), table geometry, physics (`Sim`), game rules (`game`), editor, inspector, paint, modes, cameras, dialogs, and the main loop.

To add a new part type:
1. Add an entry to `PARTS` (defaults and inspector fields).
2. Add a mesh builder to `BUILD`.
3. Add its collision shape in `Sim.add`.
4. Add its picking shape in `outline()`.
5. Add a button to `TOOL_DEFS`.

`window.PCK` is a debug handle exposing the scene, simulation and game state. `PCK.step(seconds)` advances the physics without rendering, which is useful for testing.

## Credits

Inspired by *Pinball Construction Set* by Bill Budge, published by Electronic Arts in 1983. This is an independent fan homage and is not affiliated with Electronic Arts. Rendering by Three.js. Fonts from Google Fonts: Inter, Orbitron, VT323, Bungee and Monoton.
