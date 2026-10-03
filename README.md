# Woodturning sim (Lathe Lab)

A simulator for seeing what happens when you turn a blank on different axes. One self-contained HTML file with no build step and no dependencies.

**Live: https://cameronlinton03.github.io/woodturning-sim/** (or open `index.html` in a browser).

- **Cut like a lathe game.** In the side view, move the tool (left/right is along the blank, up/down is depth) and hold the button to cut. Roughing gouge, spindle gouge and parting tool (keys 1 to 3).
- **Blanks.** Square, triangle, pentagon, hexagon, octagon, plank, cylinder, oval, with adjustable size and length.
- **Mounting.** Drag the centre dot in the end view to mount off-centre, or tick "skew axis" to move the headstock and tailstock centres separately. Press Remount after cutting to turn a second axis (multi-axis turning).
- **Readouts.** Wood left, whether the cut is in the air, interrupted or continuous, the flats-to-corners range under the tool, and static and rocking imbalance (rule-of-thumb bands, not engineering limits).
- **Views.** Side view (the workbench), end-on section under the tool, and a WebGL2 ray-marched 3D view.

Keys: Space starts/stops the lathe, Z undoes.

**On a phone or tablet:** touch the side view and drag to cut (the tool tip sits above your finger so you can see it). The end view scrolls with the page; tap *Move axis centre* to drag the axis dot instead. In the 3D view, drag sideways to orbit and pinch to zoom. Landscape gives a bigger workbench. Depth is about one pixel per millimetre in portrait, so for fine cuts use landscape or a larger screen.

## How it works

The blank is a prism mounted on an axis (a line between centre points on its two end faces). Each mount keeps a radius profile along its axis, and a tool pass sets `r(t) = min(r(t), tool outline)`. The wood left is the blank intersected with every mount's profile solid, so remounting on a new axis simply adds another solid. No mesh, so nothing degrades as you cut. The end view (CPU, per pixel) and the 3D view (GLSL) read the same field; keep `mountD()` in the JS and in the shader in step. See the comment at the top of the script for the full model.
