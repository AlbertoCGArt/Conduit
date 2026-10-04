# Conduit

Cable dressing for hard-surface scenes in Blender. Cables that hang between
anchors, fan out from a hub, drop from a ceiling and sprawl across the floor,
or get drawn straight onto a surface. They end in real hardware and bake down
to a game-ready mesh with UVs.

**[Get Conduit](https://3dartstuff.com/conduit)** ·
[Report a bug](https://github.com/AlbertoCGArt/Conduit/issues/new/choose) ·
[Changelog](CHANGELOG.md)

This repository is Conduit's manual and issue tracker. The add-on itself is
sold at [3dartstuff.com/conduit](https://3dartstuff.com/conduit).

## Install

1. **Edit ▸ Preferences ▸ Add-ons ▸ Install from Disk**, pick `conduit_<version>.zip`.
2. Enable **Conduit**.
3. The panel is in the 3D viewport sidebar (`N`), under the **Conduit** tab.

Needs **Blender 4.5 LTS or newer**. Every release is tested on 4.5 LTS and on
the newest Blender.

## The four cable modes

The panel has one tab per mode. Each tab has its own list of layers — a layer
is one cable setup with its own look, anchors and output — and its own
selection.

### Hang — cables between anchors

A catenary between two or more anchor empties, with slack.

1. **Place Anchors** creates a starting pair, or **Pick** places anchors
   directly on a vertex, edge or face of your geometry (they stick to it).
2. Move the anchors, then **Generate Cable**. From then on, dragging an anchor
   or changing a setting rebuilds the cable live. If two anchors of a span sit
   in the same place, Generate names them: that span has no length to show.
3. **Add Point** inserts an anchor between two selected ones. On an A to B
   layer with one cable, that cable becomes a chain through all three; with
   several, set **Spans** to **Chain** first.
4. **Remove Point** (**−** beside Add Point) takes the selected anchors out
   and the cable closes up over the gap. On A to B the whole cable goes, both
   anchors. A drop on a span that no longer exists goes with it. An empty of
   your own is taken out of the cable but left in the scene.

Options:

- **Chain** runs one cable through every anchor in order. **A to B** pairs the
  anchors up and makes one cable per pair, each its own object — click one in
  the viewport and the panel edits that cable.
- **Several cables on one chain**: **New Cable** adds another cable along the
  same anchors, with its own look. **Together** bundles them, **Spread** lays
  them side by side like a cable tray, **Manual Offset** places each one.
- **New Chain** starts a separate cable with its own anchors, leaving the
  existing ones alone.
- **Slack**, per-span **sag variance** and a **seed** control the hang.
- **Drop** a span of a hanging cable to the floor: *End* lets the end fall and
  sprawl, *Middle* drops a loop from the middle while keeping both ends
  attached, with a controller empty you can drag.

### Fan — one hub to many targets

1. **Add Main** places a hub empty at the 3D cursor, or **Set Selected** uses any empty you
   select — a hang anchor included, to branch a fan off a chain.
2. **Pick Face** and click a face: target anchors are scattered across it.
   While you hover, the face lights up and white dots show where the targets
   will land, sized to your Resolution Scale. Scroll to change the count while
   picking. **Add Targets** picks another face without losing the first.
3. **Generate Fan Cables**. Slack is randomised between **Min** and **Max**.

Dragging the hub or any target rebuilds the fan live.

**Drop to Floor** brings fan cables down: pick the **Floor**, then choose
*From the End* (the target end has come loose and sprawls on the floor) or
*From the Middle* (the slack settles on the floor, both ends stay put).
**Chance** sets how many of the cables come down; raising it adds to the ones
already down rather than reshuffling them. The hub end always stays up.

### Draw — trace a cable across a surface

**Draw Cable on Surface**, then drag across any mesh. The cable follows the surface,
offset by **Surface Offset**. **Extend** adds to the stroke, **Erase** rubs part
of it out, **Redraw Stroke** starts over. Draw on one object, a collection, or
anything visible. **Freeze** protects hand edits to the curve from being
overwritten.

### Drop — a bundle falling from a ceiling

For cable that has come down from a ceiling point and piled up on the floor.

1. Snap the 3D cursor to a ceiling face (`Shift+S`), then **Ceiling from Cursor**.
2. Pick the **Floor** mesh. Landings raycast against that mesh only, from the
   ceiling point down, so the floor has to be below it.
3. Set **Cables** and **Spread**, then **Place Landings**. Drag any landing to
   steer that one cable; **Reseed** rerolls them all.
4. **Generate Drop Cables**. A landing dragged up to or above the ceiling has
   nowhere to fall to: that cable is left out, and Generate says how many were.

Shape: **Fall Bow** (waver on the way down), **Floor Bend** (how widely it
curls over on landing), **Sprawl Min/Max** (how far it runs once down),
**Waviness**, and **Detail** (sampling only — finer draws the same run more
smoothly, not a curlier one). A cable on the floor never bends tighter than
about twelve times its own thickness: it curves away from walls, the floor's
edge and other cables instead of folding against them, and ends where it is
boxed in.

- **Landing Chance** below 1 leaves some cables hanging short, cut ends and all.
- **Avoid Obstacles** keeps falls and floor runs out of walls and props. Leave
  **Colliders** empty to use every visible mesh except the floor, or name
  collections to keep it fast in a heavy scene. **Objects** adds single
  objects instead — select a few props and click it. A bevelled curve (a
  pipe) counts; a curve with no bevel is a line and is ignored. A pipe with
  no end caps still counts as solid. A room you are *inside* is
  recognised as a room, not a crate to be pushed out of. Delete a collider
  and it is gone from the list for good — a new object that takes its name
  is not picked up.
- **Avoid Crossings** keeps floor runs from passing through each other.
- **One cable that differs**: click a cable, **Override Selected Cable**, and
  the profile block edits just that cable. **Edit Every Other Cable** goes back.

## The look: profiles

Every layer has a cable profile — the cross-section and what it does along its
length.

- **Preset gallery**: Power Cable, Thin Wire, Rope, Braided Cable, Ribbon
  Cable, Flat Strap, Rigid Pipe, Hose, Corrugated Hose, Cable Trunking, I-Beam,
  Twisted Bar, Tapered Vine, Damaged Loom, Wire Harness. A preset is a starting point; tweak
  anything after.
- **Shape**: Round, Square, Rectangle, Hexagon, N-Gon, Pipe, Teardrop,
  L-Angle, U-Channel, I-Beam, or any curve you pick. **Strands** turns one
  cable into a twisted rope, braid or ribbon bundle.
- **Harness** (its own section under the profile): many cables in one run,
  held together by **zip ties**, **tape** or **velcro**. Build it from rows —
  *7 thin Plain, 1 Twisted Pair, 3 thick Plain, 1 Braid* — each with its own
  count, size, material and share of **Loose** cables. Against repetition:
  **Tie Jitter** and **Missing Ties** break the spacing, **Wander** lets
  cables drift across the bundle, **Loose per Gap** makes a loose cable sag in
  some gaps and not others, and zip-tie **Heads** face at random or all one
  way. The rows save with the profile, so a harness goes into your library. Works in every mode: a hanging
  harness, a fan of them, or one dropped from the ceiling and lying on the
  floor, where it opens out sideways instead of sagging into it. The **Wire
  Harness** preset starts you off.
- **Per metre** detail — rope lay, roll, ribbing — holds its pitch at any cable
  length.
- **Taper**, thickness noise, tilt.
- **Damage**: worn-through jacket with the copper conductor showing.
- **Library**: **Save** a profile and **Load** it in any file. **Copy From
  Layer** borrows another layer's look. Point every Blender version at one
  library folder in Preferences.

## Ends

How a cable leaves its anchor, and how it finishes. Set per end, or both at
once.

- **Exit**: by default a cable sags from the anchor itself. *Square To Surface*
  leaves the surface the anchor was picked on at a right angle, runs straight
  for **Straight Run**, then bends at **Bend Radius** (default: four times the
  thickness). *Aim* uses the anchor empty's +Z — rotate the empty to point the
  cable. *Into Surface* dives into the wall.
- **Style**: *Plain*; *Stripped* cuts the jacket back and shows coloured cores
  and bare copper; *Frayed* splays and droops them; *Heat-Shrink* and *Taped*
  put a band over the end.
- **Uneven Cut** (a harness or a rope): a cut bundle is never cut flush. Each
  wire ends in its own place, **Broken** snaps a share of them off shorter
  still with the copper showing, and **Splay** and **Droop** let what is left
  open out of the bundle and hang. An end that hangs from its anchor keeps one
  wire running to it, the way a stripped end keeps one core.
- **Break Out**: the last stretch splits and every wire goes to its own
  terminal — every cable in a harness, every strand of a rope, or the cores of
  a single cable. **Split Length** is how far back it starts. Either pick
  **Terminals** of your own (objects, in order: a connector's pins, a terminal
  strip, the studs on a busbar) or leave it to lay out a block for you,
  **Terminal Spacing** apart in as many **Rows** as you ask for, centred on the
  anchor and turning with it. Every wire arrives square to its terminal and
  none crosses another to get there, the ties stop before the split, and
  **Boot** wraps it where it comes apart. A fitting on that end goes on every
  wire instead — a ferrule or a lug sized to the wire it crimps, not to the
  bundle it came out of.

## Fittings & Clips

- **Fitting** at either end: a built-in **Gland, Plug, Lug, Ferrule** or
  **Grommet**, or any object of your own. It sits on the anchor facing out
  along the cable and scales with cable thickness, so one fitting works for
  every cable. **Inset** makes the cable enter the fitting instead of stopping
  at its face, in every mode. On a cable too short for it, the inset is
  shortened to fit, and Generate (Rebuild Cable on the Draw tab) tells you.
- **Clip** repeated along the cable. A hanging span is held at its anchors, so
  that's where clips go. **Spacing** is for cable that rests on something — a
  drawn stroke or a drop's floor run — and clips lie flat against that surface.

Fittings and clips are rebuilt as you drag, updated in place (a material you
assign to one survives), and bake with the cable on Finalize.

## Viewport Detail

Every layer has a **Full / Medium / Low** switch under its list, with the
face count it costs beside it. Full draws everything the profile asks for;
Medium and Low thin the rings and round sides for heavy shots. The globe button sets
every layer in the scene at once. It renders at the level you pick, so set
Full before the final render. The bake uses its own settings and never this.

A harness is light at Full anyway: its rings go where the cable bends, sags
or twists, not every few millimetres along it.

Past about half a million faces the count turns red and Generate warns you.
The cable is still built in full — nothing is coarsened behind your back —
so lower the detail, or split a very long run into shorter ones.

## Finalize — bake to mesh

Turns a layer into a mesh for export.

- Its own resolution — **Length Steps** and **Round Sides**, and **Harness
  Detail** for a harness — independent of the viewport. A layer left on Low
  still bakes at what Finalize says.
- **World Length UVs**: U is arc length divided by **Tile Length**, so every
  cable in the scene has the same texel density. Seams are offset per cable.
- **One mesh per layer** (one draw call) or one per cable. The triangle count
  is shown.
- The curves are **hidden, never deleted**: change anything and finalize again.
  Modifiers and materials you add to the baked mesh survive a re-finalize.
- **Detach Mesh** hands the mesh over to you for good.
- A cable with no faces — two anchors in one place, say — is skipped with a
  warning rather than baked into an empty object.

## Preferences

**Edit ▸ Preferences ▸ Add-ons ▸ Conduit**:

- **Profile Library** — where saved profiles live. Point every Blender version
  at the same folder.
- **Live Delay** — how long live preview waits before rebuilding. Raise it on a
  heavy scene.
- **Panel Tab** — which sidebar tab the panel sits under.

## Good to know

- **Everything Conduit makes is tagged.** It only ever clears or deletes what it
  generated. A collection of yours that happens to share a name is never
  touched.
- **Rename anything.** Layers hold real references, so renaming an anchor,
  floor or output in the outliner doesn't break anything.
- **One collection per layer.** Everything Conduit makes goes under a
  `Conduit` collection, in a collection named after its layer, with its
  anchors, hub, targets and drop controllers in `<layer>_Controls`. Rename the
  layer and both collections follow (unless you renamed one yourself). Delete
  the layer's collection and keep its contents, and new anchors still join
  the same Controls. File everything somewhere of your own and Conduit leaves
  it there — it doesn't bring back an empty collection. The outliner button
  in the panel header tidies anything left loose in the scene root. Things
  you filed in collections of your own are never moved.
- **Removing a layer (−) removes everything it made**: its cables, anchors,
  hub and targets, fittings and clips. A **finalized mesh stays** — baked work
  is yours. So does an empty of your own that a layer only pointed at, and
  anything another layer still uses (a chain anchor that is also a fan's hub).
- **Delete a generated cable** and the next Generate puts it back. Convert one
  to a mesh and it's yours — Conduit leaves it alone.
- **Scene ▸ New ▸ Copy Settings** is safe: cleaning up the copy never deletes
  the original shot's cables.
- Live preview pauses in Edit Mode.
- **Pick**, **Pick Face** and **Draw Cable on Surface** start only in the 3D
  viewport.
- Hover any button or setting for a tooltip.

## Support

- **Bugs and feature requests:** [open an issue](https://github.com/AlbertoCGArt/Conduit/issues/new/choose).
  It needs a free GitHub account. Include your Blender and Conduit versions
  and, if you can, a small .blend in a .zip.
- **Your purchase and downloads:** [3dartstuff.com/conduit](https://3dartstuff.com/conduit).
