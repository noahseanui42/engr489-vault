# Mechanical / Structure

Current state. Overwrite as things change; log changes in [[worklog]].

## Top plate
6 mm acrylic (prototype) → 6 mm aluminium (final). Prototype sent for laser cutting.
- Three-lobed outline, central hole, three radial arm slots from ~mid-radius to the rim
  (open-ended at rim), each with a small square notch at the inner end.
- Servos mount **flush underneath** (no standoff); upper arm sweeps up *through* the plate.
- 40 mm tangential slit per arm (servo horn sits 10 mm out from the servo body).
- **Note:** flush-mount through-slots break the plate's hoop path — remediation via
  standoffs or frame-bolted lobes. → [[open-issues]]

## Bicep (proximal arm)
Hollow box 20×25 mm, 3 mm walls, ~210 mm printed (180 mm connection-to-connection;
extra each end for servo-horn mount + elbow connection).

## Elbow
Fork/clevis in double shear; yoke boss with V-splayed faces (print-orientation +
non-magnetic fasteners settled Apr–Jun 2026 build phase).

## 3D printing
Apply **+0.2 mm hole diameter correction** for printed parts taking fasteners/rod ends.

## Stand
Three 2020 aluminium extrusion legs at 120°, circumradius ~433 mm for a 750 mm triangle.

## SolidWorks
DXF for laser, STL for print. Circular Component Pattern for 120° arms; Ball mates for
spherical joints; parallelogram forearms. **Disable Shadows / Ambient Occlusion** — this
assembly crashes otherwise.

Related: [[rod-ends-joints]], [[kinematics]]
