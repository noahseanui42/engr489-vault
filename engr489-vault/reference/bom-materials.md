# Materials & BOM

Current state. Overwrite as things change; log changes in [[worklog]].

> **Hard constraint:** non-ferromagnetic and non-conductive near the probe. The robot
> sits inside an active Helmholtz coil — magnetically-responsive material corrupts the
> measurement. Flag any part with iron/nickel/cobalt content before committing.

**Allowed:** PLA, PETG, carbon fibre, aluminium, nylon/plastic fasteners.
**Avoid:** steel fasteners, standard bearings, any ferrous hardware.
**Live exception:** SI6T/K steel-ball rod ends (prototype only). → [[rod-ends-joints]]

## Suppliers
- **RS Components** — nylon M6 nuts, rod-end hardware
- **Hobby Corner NZ** — carbon fibre tubes, servo extension cables
- **Nicegear NZ** — Adafruit 16-ch PWM/Servo Shield
- **element14** — Arduino UNO R4 **Minima** (R4 WiFi avoided — RF interference near magnetometer)
- **Small Parts & Bearings** — rod ends

Related: [[rod-ends-joints]], [[servos]]
