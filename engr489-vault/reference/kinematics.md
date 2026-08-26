# Kinematics

Current state. Overwrite as things change; log changes in [[worklog]].

Geometry adapted from `grzesiek2201/Delta-Robot` (GitHub), cross-checked against a Python sim.

## Confirmed build parameters
- `sb` = 450 mm (base triangle side)
- `sp` = 18 mm (platform triangle side)
- `L`  = 180 mm (proximal arm / bicep, connection-to-connection)
- `l`  = 600 mm (distal rod length)

## Gotcha
Inherited code had hardcoded `sb=567 / sp=76 / L1=524 / L2=1244` — **wrong**, already
fixed to the values above. If a script misbehaves, check it isn't reverting.

## Status
Reachable depth ~276 mm — **24 mm short** of the 300 mm target for z ∈ [−450, −750] mm.
Geometry revision options identified, not yet chosen. → [[open-issues]]

Related: [[servos]], [[mechanical]]
