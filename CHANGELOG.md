# Changelog

## 1.0.1 — 2026-10-03

Polish.

- Disabling the add-on no longer leaves a pending rebuild to fire into it.
- Viewport overlays keep their line width on Metal and Vulkan, and their text
  follows your Resolution Scale.
- Fan's Pick Face and Draw on Surface only start in a 3D View.
- A layer's Controls collection is renamed with the layer; deleting a layer's
  collection no longer splits its anchors in two; and a layer whose things you
  filed elsewhere no longer gets an empty collection back on every rebuild.
- Anchors in the same place, a Fitting Inset clamped on a short cable, and a
  heavy cable (past half a million faces) are now reported. Heavy cables are
  still built in full; the face count in the panel turns red.
- Nothing is baked from a cable with no faces.
- A Drop floor above the ceiling gives no landings, and a landing dragged
  above it is left out and reported.
- A deleted collider's name no longer makes a new object of that name an
  obstacle.
- Tooltips on every button and setting.
- Generated materials no longer use the deprecated Material.use_nodes.

## 1.0.0 — 2026-10-03

First release.

- **Four cable modes:** Hang, Fan, Draw and Drop.
- **Wire Harness:** build a harness from rows of cable types, held by zip
  ties, tape or velcro, with loose cables that sag between the ties.
- **Profiles:** 15 presets, any shape or curve of your own, and a profile
  library you can share between Blender versions.
- **Ends:** Square To Surface, Aim and Into Surface exits; stripped, frayed,
  heat-shrink and taped ends; uneven cuts; Break Out to individual terminals.
- **Fittings and clips:** gland, plug, lug, ferrule, grommet, or any object
  of your own.
- **Drop to Floor** for hanging and fan cables, with obstacle avoidance.
- **Viewport Detail:** Full, Medium or Low, with the face count beside it.
- **Finalize:** bake to a game-ready mesh with world-length UVs, one mesh per
  layer or per cable.
