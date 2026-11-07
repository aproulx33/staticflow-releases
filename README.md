# StaticFlow

**Free body diagrams you can solve, not just draw.**

StaticFlow is a Windows desktop tool for 2D statics. You lay out the bodies,
supports, loads and members on a canvas, connect them up, and press F5 - and the
same drawing hands back reactions, member forces, a closed free body diagram for
every component, and bending stress with a factor of safety.

It exists because the free body diagram on the whiteboard and the numbers in the
spreadsheet drift apart the moment anything changes. Here the diagram *is* the
analysis: move a load, press F5, and everything downstream of it moves too.

This repository is the **download page**. The source lives elsewhere.

---

## Download

[**Get the latest build from the Releases page**](../../releases/latest)

Windows 10 or 11, 64-bit. Download **`StaticFlow-<version>-win64-setup.exe`**
and run it. It installs for your user only (no administrator prompt), adds a
Start-menu entry, and opens `.sfp` and `.sff` files from Explorer.

**Windows will say "Windows protected your PC."** Click *More info*, then *Run
anyway*. These builds are not code-signed yet, and SmartScreen flags any
executable it has not seen before. Every release lists its files' SHA-256, so
you can check what you downloaded:

```
certutil -hashfile StaticFlow-<version>-win64-setup.exe SHA256
```

**It keeps itself up to date.** Once installed, StaticFlow checks for a newer
beta at most once a day and offers to install it in place, after offering to
save your work. Help > Check for Updates asks on demand. The check sends
nothing about you. Uninstall from Settings > Apps.

### The portable zip

Each release also has `StaticFlow-<version>-win64.zip`, which installs nothing.
**Unblock it before extracting** (right-click, Properties, tick **Unblock**) and
**extract the whole folder**: run straight from the zip preview, the exe fails
with "Qt6Gui.dll was not found". A zip copy tells you when a new beta is out but
sends you here to get it. `README.txt` inside covers setup, feedback and
uninstalling.

---

## What it does

- **Solve, on demand.** Rigid-body statics - sum of Fx, Fy and M - over as many
  sub-assemblies as your model has, each reported independently. Solving is
  never automatic: you edit freely, then ask.
- **A closed FBD for every component.** Not one global diagram: focus any beam,
  bracket, sheave or support and see the arrows that close on it.
- **Ropes that route.** One rope is an ordered run of waypoints over sheaves and
  through blocks, and the tension ratios come out of the routing - a four-line
  block and tackle reports its 4:1 without being told. Ropes sag, slip, lift
  off a slack rim and carry sheave friction.
- **Whole structures.** Beams, trusses and springs are solved by a stiffness
  method: member forces, deflections, and indeterminate structures.
- **Imported parts.** STL and STEP solids with their mass properties, connected
  and dimensioned on their real features.
- **Reports and scenarios.** A PDF calculation report, PNG/SVG export, load cases
  with multipliers and sweeps, and side-by-side comparison.
- **Bolted joints.** Bolt groups checked to AISC 360-22 or EN 1993-1-8, and a
  Fastener Analysis tab for bolt and screw patterns.
- **Solve backwards.** Tick *Solve Magnitude* on a point load and its magnitude
  becomes the unknown: what force holds this up?
- **Real sections and materials.** Cross-section shape and dimensions give A and
  I; a per-project material library gives the stress tab a factor of safety.
- **Dimensions and angle constraints**, an offline 57-page manual, and per-field
  context help.

---

## Start with the samples

Every build ships five worked models in `samples`. Open one with
**File > Open** and press **F5**:

| sample | what it shows |
|--------|---------------|
| `tower-crane.sfp` | rope over a sheave, tie member, fixed base, counterweight |
| `drilling-rig-block.sfp` | 4-line block and tackle - the 4:1 falls straight out |
| `roof-truss-snow.sfp` | truss members, drifted snow load, zero-force members |
| `bridge-settled-pier.sfp` | an indeterminate girder, through the stiffness core |
| `excavator-arm.sfp` | hydraulic actuators - solving for cylinder force |

The samples folder's own `README.md` gives the number each one **should**
produce, worked by hand. If you get something else, that is a bug and worth
reporting.

---

## This is a beta

Pre-release software, handed out to get used on real problems. Expect rough
edges, and expect to report them.

- A cable's Tension is an input you type, not a solved unknown. Use a truss
  member or a rope to have the force solved.
- The `.sfp` save format is still changing - files saved by one beta may not
  open correctly in the next.
- Not code-signed, and no crash reporter yet.

Each release page lists the limits for that specific build.

**Feedback goes through Help > Contact Support inside the app**, which reaches
the author directly. Include the build string from Help > About StaticFlow, and
the `.sfp` if you can. "I could not work out how to do X" is the most useful
report there is.

---

## License and a warning

Provided as-is for evaluation - see `LICENSE.txt` in the download. Built with
the [Qt framework](https://www.qt.io) under the LGPLv3.

**StaticFlow's results are not certified and have not been independently
verified.** Do not lean on a number this program gives you for a design,
construction, lifting or safety decision without checking it yourself. During a
beta, that goes double.

Copyright (c) 2026 Adam Proulx. All rights reserved.
