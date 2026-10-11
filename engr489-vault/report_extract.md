# report_extract.md — evidence extracted from `engr489-vault`

Date of extraction: 2026-10-11. Citations are `file:line` relative to `engr489-vault/engr489-vault/` (the vault folder), or a commit hash.

## 0. Read this first: what the repo contains

Your brief assumed code, data files, plots and a multi-commit history. **This repo has none of those.**

- **One commit**: `44b4a26`, 2026-08-26 15:19:55 +1200, message "intial vault" (sic). It adds 20 files, 492 lines.
- **No source code.** There is no firmware, Python, MATLAB or C++ in it. `reference/firmware.md:5` says the firmware lives in a separate `engr489-firmware/` repo, which is not here.
- **No data files and no result plots.** The only image is one architecture block diagram (§7).
- **No CLAUDE.md.** There are no test files either.
- **The vault is the notes migration, not the project record.** The worklog has one entry, which says the year's notes were migrated into reference files (`worklog.md:19-20`). Every value in `reference/` is a snapshot as of 2026-08-26 (`README.md:9-11`).
- Content from before 2026-08-26 is undated. The only internal date clue is "Apr–Jun 2026 build phase" (`reference/mechanical.md:20`).

**Consequence for the report.** Almost none of the skeleton's Section IV numbers have any evidence here. Examples: 3.4° → 0.51°, 2.3 mm rms, 180 nT, 1.3 mm, 33 mm offset, the 27 tests, and all of Figs. 2–14. Those must come from the firmware/analysis repo, the GitLab repo named in your Appendix A, or your lab data. Do not cite this vault for them.

**File naming.** You referred to `skeleton.md` and `sources.md`. The attached files are `Report.md` (skeleton) and `ENGR489_Literature_Notes.md` (sources). I used those.

**Coverage of sources.** I read the Literature Notes index and the first 657 lines. I also searched all 2152 lines by heading and keyword. I did not read every note in full, so the "not in sources" flags in §8 rest on the index and keyword searches.

---

## 1. Repo purpose and active date range

**Purpose.** An Obsidian note vault for the ENGR489 capstone: a robotic platform that maps magnetic field inside a Helmholtz coil system. It is a documentation structure, not a codebase.
- Structure: current-state reference notes, an append-only worklog, and a live checklist (`README.md:7-15`, `README.md:27-32`).
- Hard design constraint: non-ferromagnetic and non-conductive near the probe, because the robot sits inside an active coil (`reference/bom-materials.md:5-7`).

**Active date range from git.** 2026-08-26 only (`44b4a26`). The worklog also has only that date (`worklog.md:18`).

**Not recoverable from this repo.**
- The March 2026 proposal, the gantry → delta change and the Oct 2026 scope change in skeleton I-B.
- Everything after 2026-08-26.

**Stated vault conventions.**
- ISO dates (`README.md:19-20`).
- Binaries go in `assets/`, which is "not committed to git" (`assets/README.md:3`, `README.md:32`). So CAD, STL, DXF, photos and datasheets are absent by design.
- The repo's README says "Mixing these two is what caused the mess all year" (`README.md:15`). That is the only statement of why the vault was restructured.

---

## 2. Timeline of key changes

| Commit | Date | Change |
|---|---|---|
| `44b4a26` | 2026-08-26 | "intial vault": adds the reference notes (kinematics, mechanical, servos, rod ends, BOM, firmware), `worklog.md`, `open-issues.md`, the Obsidian config, one architecture PNG plus a canvas that embeds it, and two empty Obsidian placeholders |

That is the whole git history. `git log --reverse --stat` returns this one entry.

Dated events in note text, with no commit behind them:
- 2026-08-26: vault set up and notes migrated (`worklog.md:18-24`).
- Apr–Jun 2026: elbow print-orientation and non-magnetic fasteners "settled" (`reference/mechanical.md:19-20`).

---

## 3. Design decisions: chosen, rejected, why

The rationale column says "not recorded" wherever the vault gives no reason.

| Decision | Chosen | Rejected / alternative | Rationale | Cite |
|---|---|---|---|---|
| Material policy | PLA, PETG, carbon fibre, aluminium, nylon/plastic fasteners | Steel fasteners, standard bearings, ferrous hardware | Magnetically responsive material "corrupts the measurement" inside an active coil | `reference/bom-materials.md:5-10` |
| Rod ends | SI6T/K M6×1.0 steel-ball female rod ends, **prototype only** | Non-magnetic rod end (wanted, not yet sourced) | Only "accepted compromise for the first prototype"; the reason it was accepted is not recorded | `reference/rod-ends-joints.md:5-8`, `reference/bom-materials.md:11`, `open-issues.md:6` |
| Rod-end to tube joint | Bore out the M6 thread in the rod-end shank and epoxy the CF tube in directly | Stud or ferrule (explicitly "no stud or ferrule") | Mismatch: M6 female thread minor Ø 4.95 mm vs 6 mm CF tube OD | `reference/rod-ends-joints.md:10-12` |
| Turnbuckle adjustment | None | — | Constraint, not a choice: right-hand thread on both ends | `reference/rod-ends-joints.md:13` |
| Microcontroller | Arduino UNO R4 **Minima** | R4 WiFi | "RF interference near magnetometer" | `reference/bom-materials.md:17` |
| Servo drive | PWM direct from Arduino D9/D10/D11 | Adafruit 16-ch PWM/Servo Shield (still in the BOM, "unused for bring-up") | Rationale not recorded | `reference/servos.md:7-8`, `reference/bom-materials.md:16` |
| Actuators | 3× Futaba S3306MG | Rationale not recorded (skeleton III-D gives "servos not steppers", but that text is not in this repo) | not recorded | `reference/servos.md:5` |
| Servo power | "6V 4×AA pack", common ground with the Arduino | — | not recorded | `reference/servos.md:9` |
| Servo feedback | Internal pot tapped with feedback wires, read on A0 with no divider | — | Wiper range 0.8–2.23 V is safe for the ADC input | `reference/servos.md:11-12` |
| Bring-up control approach | Four phases ending in "closed-loop `moveTo` with proportional pulse trim" | — | Rationale not recorded | `reference/servos.md:23-27` |
| Servo timing | Blocking `delay()` acceptable for 1 servo; rework to `millis()` before 3 | — | Only a scaling concern | `reference/servos.md:29`, `open-issues.md:9` |
| ADC resolution | 12-bit "sufficient"; using 14-bit | — | "noise-averaging headroom" | `reference/firmware.md:8` |
| Kinematics source | Geometry adapted from GitHub `grzesiek2201/Delta-Robot`, cross-checked against a Python sim | — | not recorded | `reference/kinematics.md:5` |
| Top plate | 6 mm acrylic (prototype) → 6 mm aluminium (final); servos flush underneath; arms sweep up through radial slots | Standoff-mounted servos (implicit) | Reason for flush mount not recorded | `reference/mechanical.md:6-10` |
| Top-plate hoop-path problem | Open; options are standoffs or frame-bolted lobes | — | The slots break the plate's hoop path | `reference/mechanical.md:11-12`, `open-issues.md:8` |
| Bicep | Hollow box 20×25 mm, 3 mm walls | — | not recorded | `reference/mechanical.md:14-16` |
| Elbow | Fork/clevis in double shear, V-splayed yoke boss | — | not recorded | `reference/mechanical.md:18-20` |
| Stand | Three 2020 aluminium extrusion legs at 120° | — | not recorded | `reference/mechanical.md:25-26` |
| Embedded target | RA4M1: USB CDC serial, GPT timers for PWM, 48 MHz HOCO → PCLKD/PCLKB/USBFS | — | not recorded | `reference/firmware.md:9-10` |
| Host–Arduino interface | Line-based ASCII over USB CDC | — | not recorded; **conflicts with skeleton**, see §10 | `delta_robot_field_mapping_architecture.png` |
| Servo library | `VarSpeedServoRA4M1` | — | not recorded | `delta_robot_field_mapping_architecture.png` |

**Rejected options.** The repo does not record alternatives such as gantry vs delta, steppers vs servos, or the from-scratch control stack. Skeleton III-D/F/G "Alternative considered" paragraphs have no support here.

---

## 4. Quantitative results and parameters

Every number in the vault is listed below. There are no measured results, only parameters and targets.

### Geometry (as of 2026-08-26; superseded per skeleton, see §10)

| Quantity | Value | Cite |
|---|---|---|
| `sb`, base triangle side | 450 mm | `reference/kinematics.md:8` |
| `sp`, platform triangle side | 18 mm | `reference/kinematics.md:9` |
| `L`, bicep (connection-to-connection) | 180 mm | `reference/kinematics.md:10` |
| `l`, distal rod | 600 mm | `reference/kinematics.md:11` |
| Inherited hard-coded values labelled "wrong" | sb=567, sp=76, L1=524, L2=1244 | `reference/kinematics.md:14-15` |
| Reachable depth | ~276 mm | `reference/kinematics.md:18`, `open-issues.md:5` |
| Depth target | 300 mm for z ∈ [−450, −750] mm | `reference/kinematics.md:18` |
| Shortfall | 24 mm | `reference/kinematics.md:18`, `open-issues.md:5` |

### Mechanical

| Quantity | Value | Cite |
|---|---|---|
| Top plate thickness | 6 mm (acrylic prototype, aluminium final) | `reference/mechanical.md:6` |
| Tangential slit per arm | 40 mm | `reference/mechanical.md:10` |
| Horn offset from servo body | 10 mm | `reference/mechanical.md:10` |
| Bicep section | 20 × 25 mm, 3 mm walls | `reference/mechanical.md:15` |
| Bicep printed length | ~210 mm (180 mm connection-to-connection) | `reference/mechanical.md:15-16` |
| Print hole correction | +0.2 mm hole diameter | `reference/mechanical.md:23` |
| Stand circumradius | ~433 mm for a 750 mm triangle | `reference/mechanical.md:26` |
| Leg angle | 120° | `reference/mechanical.md:26` |
| CF tube | 6 mm OD / 4 mm ID | `reference/rod-ends-joints.md:9` |
| M6 female thread minor Ø | 4.95 mm | `reference/rod-ends-joints.md:10` |
| Rod-end thread | M6 × 1.0 | `reference/rod-ends-joints.md:5` |

### Servos and electronics

| Quantity | Value | Cite |
|---|---|---|
| Servo count | 3 | `reference/servos.md:5` |
| Control pins | D9, D10, D11 | `reference/servos.md:7` |
| Supply | 6 V, 4×AA | `reference/servos.md:9` |
| Pot wiper voltage | 0.8 V at 800 µs; 2.23 V at 2200 µs | `reference/servos.md:11-12` |
| Travel limits | 800–2200 µs (1400 µs span, symmetric about 1500 µs) | `reference/servos.md:14` |
| Working calibrated limits | ~830–2170 µs | `reference/servos.md:14-15` |
| Calibration sketch serial | 115200 baud, newline-terminated | `reference/servos.md:20` |
| Calibration fit | `angle = a·counts + b` | `reference/servos.md:19` |
| ADC | 12-bit sufficient, 14-bit used | `reference/firmware.md:8` |
| Clock | 48 MHz HOCO | `reference/firmware.md:10` |

### Not in the vault

None of these skeleton values has any support here (all in §10):
- Joint calibration constants c_i, k_i (skeleton Table VI).
- β coefficients.
- Joint limits (−20° to +70°).
- ω_max = 90°/s.
- The 5 s settle time.
- Torque and rated-torque figures.
- All Section IV results.

---

## 5. Test procedures and methods actually used

The vault records plans and tooling, not executed tests.

- **Servo calibration sketch** `servo_calibration_v3.ino` (the sketch itself is not in this repo).
  - D9 only, Servo library with EEPROM storage (`reference/servos.md:18-19`).
  - Linear fit of angle against counts, with counts compared to a protractor reading (`reference/servos.md:19`).
  - Serial commands `u / a / + / - / [ / ] / c / s / p / w / r` (`reference/servos.md:20`). The vault does not say what each does.
  - Hard limits 800–2200 µs, with A0 pot feedback (`reference/servos.md:21`).
- **Bring-up plan**: Phases 0–4 with exit criteria D1–D6 (`reference/servos.md:23`). Four steps are listed (`reference/servos.md:24-27`): open-loop sweep, feedback read, linear calibration vs protractor, closed-loop `moveTo`. The D1–D6 criteria themselves are not written down. The vault does not say whether any phase was completed.
- **Kinematics check**: geometry "cross-checked against a Python sim" (`reference/kinematics.md:5`). Method and result not recorded.
- **Print tolerance**: the +0.2 mm hole correction (`reference/mechanical.md:23`). No record of how it was found. Skeleton III-D says "found by test prints", which is not supported here.

Not in the vault: pen-and-ruler tests, the leave-one-run-out correction fit, magnetometer in-situ checks, the dipole test, repeat maps, the 27 pytest tests, and the digital protractor (0.1°) or pen-and-ruler (±1.5 mm) rigs.

---

## 6. Problems hit and workarounds

| Problem | Workaround / status | Cite |
|---|---|---|
| Inherited code hard-coded wrong geometry (567/76/524/1244) | Fixed to 450/18/180/600; warns to check scripts do not revert | `reference/kinematics.md:13-15` |
| MATLAB/Simulink duplicate functions and a parameter mismatch | Cleaned up and resolved | `reference/firmware.md:6-7` |
| Reachable depth 276 mm vs 300 mm target | **Open.** Revision options were "identified, not yet chosen" (the options are not listed) | `reference/kinematics.md:17-19`, `open-issues.md:5` |
| Steel-ball rod ends are magnetic | **Open.** A non-magnetic swap is needed before the final build | `open-issues.md:6`, `reference/rod-ends-joints.md:6-8` |
| M6 thread (minor Ø 4.95 mm) vs 6 mm CF tube | Bore out the shank and epoxy the tube in | `reference/rod-ends-joints.md:10-12` |
| No turnbuckle adjustment (right-hand thread on both ends) | No workaround. A bonding jig for equal rod pairs is **still needed** | `reference/rod-ends-joints.md:13-14`, `open-issues.md:7` |
| Flush-mount through-slots break the plate hoop path | **Open.** Standoffs or frame-bolted lobes | `reference/mechanical.md:11-12`, `open-issues.md:8` |
| SolidWorks assembly crashes | Disable Shadows and Ambient Occlusion | `reference/mechanical.md:30-31` |
| Blocking `delay()` in servo control | **Open.** Rework to `millis()` before 1 → 3 servos | `reference/servos.md:29`, `open-issues.md:9` |
| `LIBUSB_ERROR_TIMEOUT` during DFU upload on the lab machine | **Open.** Needs the WinUSB driver via Zadig, which needs admin rights. Sort it before a lab session | `reference/firmware.md:11-12`, `open-issues.md:10` |
| Publishing | Clear public project details with Dr Hollit first | `open-issues.md:11` |
| Notes messy all year | Reference/worklog split | `README.md:15`, `worklog.md:19-21` |

None of these is a record of measured behaviour (backlash, compliance, drift). Those problems from skeleton IV appear nowhere in the vault.

---

## 7. Figures: scripts, plots and data

There is **one image and no plotting scripts.**

| Figure | Evidence | Generated by | Data |
|---|---|---|---|
| `delta_robot_field_mapping_architecture.png` (2720×2480 px, 379,633 bytes) | Embedded at 520×474 on the canvas `System block diagram.canvas:3`. Not referenced from any `.md` note | Not recorded. No script or source file is in the repo. | None (a schematic) |

**What the diagram shows.**
- Blocks, top to bottom: Host computer ("IK, scan planning, logging") → Arduino UNO R4 Minima ("Parse, move, wait, report") → Servo A/B/C → Delta robot ("Moves probe end-effector") → Helmholtz coil ("Field volume being mapped"), which contains the "Magnetometer probe".
- Host–Arduino link: "USB serial (CDC, line-based ASCII)", with `MOVE a b c` going down and `DATA a b c bx by bz` coming back up.
- Arduino–servo link: "VarSpeedServoRA4M1 · PWM".
- A "readings" arrow runs from the coil back to the host.
- The diagram carries no numbers and no part names for the magnetometer.

**It conflicts with skeleton Fig. 1 / III-A**: see §10. It cannot be used as Fig. 1 without redrawing.

The skeleton's Figs. 2–14 (workspace plot, correction vectors, error plots, maps and so on) have nothing in this repo. `Untitled.canvas` (`{}`), `Untitled.base` (empty table view) and `2026-08-26.md` (0 bytes) are empty.

---

## 8. External code, libraries and papers used

Checked against the Literature Notes index (24 cite keys, shown in the sources file under Index).

| Item | Where in repo | In sources.md? |
|---|---|---|
| `grzesiek2201/Delta-Robot` (GitHub): geometry and kinematics source | `reference/kinematics.md:5` | **No.** The skeleton cites it as [9] ("upstream GUI") but there is no cite key in the index. Add it, with licence and commit. Skeleton III-J says GPL-3.0. |
| `VarSpeedServoRA4M1` library | diagram | **No** |
| Arduino `Servo` library, EEPROM | `reference/servos.md:19` | **No** (a standard toolchain item) |
| Futaba S3306MG | `reference/servos.md:5` | Yes: `futaba2010s3306mg` |
| SI6T/K rod end | `reference/rod-ends-joints.md:5` | Yes: `nzminiaturebearings2026female`. **Supplier mismatch:** the vault lists "Small Parts & Bearings — rod ends" (`reference/bom-materials.md:18`) but the source is a NZ Miniature Bearings page. |
| Arduino UNO R4 Minima / RA4M1 | `reference/bom-materials.md:17`, `reference/firmware.md:9` | **No datasheet** |
| Adafruit 16-ch PWM/Servo Shield | `reference/bom-materials.md:16` | **No.** Listed in the BOM, unused. |
| Zadig / WinUSB | `reference/firmware.md:11` | **No** (tooling) |
| SolidWorks, MATLAB/Simulink, Python sim | `reference/mechanical.md:28`, `reference/firmware.md:6`, `reference/kinematics.md:5` | **No** (tools) |
| Obsidian | `README.md`, `.obsidian/` | **No** (tool) |
| Suppliers: RS Components, Hobby Corner NZ, Nicegear NZ, element14 | `reference/bom-materials.md:14-18` | **No.** Only needed for the Table V BOM. |

Gaps between the **skeleton** and the sources index (from the skeleton's own citations, not this repo):
- Wilson 2025 [18]: no cite key.
- Phidget 1044 datasheet [14]: no cite key.
- ISO 230-2 [26].
- Tilt-correction source [27].
- Dipole-localisation source (the S. Wang 2019 TODO).
- Renaudin 2010: appears in the sources notes only as an "add to Zotero" lead.
- "Nguyen 2022": the notes point to Nguyen et al. 2015 (Neurocomputing), not 2022.

---

## 9. Mapping: skeleton section → evidence in this repo

"None" means nothing in the repo supports it.

| Skeleton section | Evidence in repo | Cite |
|---|---|---|
| I-A Problem statement | None (cage/Wilson details absent) | — |
| I-B Solution and key findings | Final-design components partly confirmed: delta, servos, Arduino R4 Minima, PLA/CF/Al. All findings: none | `reference/bom-materials.md:9`, `reference/servos.md:5` |
| I-C R1 Non-magnetic | Strong: the rule and the rod-end exception | `reference/bom-materials.md:5-11`, `reference/rod-ends-joints.md:6-8` |
| I-C R2 Scan volume | Only an older depth target (300 mm, z −450 to −750) | `reference/kinematics.md:18` |
| I-C R3–R6 | None (no budget figure; the $500 limit is not in the repo) | — |
| I-D SDGs | None | — |
| II Background | None (research notes live in the sources file) | — |
| II-H Tools | SolidWorks, MATLAB/Simulink, Python sim, Arduino: tool names only | `reference/mechanical.md:28-31`, `reference/firmware.md:6` |
| III-A Architecture | Diagram, with protocol conflicts | PNG |
| III-B Workspace modelling | Old parameters and shortfall only | `reference/kinematics.md:7-19` |
| III-C Kinematic model | Upstream source and the hard-coded-value bug. The equations themselves: none | `reference/kinematics.md:5`, `:13-15` |
| III-D Mechanical | Strong: materials, bicep, elbow, top plate, stand, rod ends, print correction, SolidWorks tips. Gaps: forearm tube is 6/4 mm CF ✓, but the 12 mm platform, 15 mm holder and 21 mm probe offset are absent | `reference/mechanical.md`, `reference/rod-ends-joints.md` |
| III-D Actuators | Part name only. Torque and rating figures: none | `reference/servos.md:5` |
| III-D Table V BOM | Suppliers only. No quantities, NZD or total | `reference/bom-materials.md:13-18` |
| III-E Electronics | Pins, supply, Minima choice, pot feedback (conflicts, see §10) | `reference/servos.md:7-12` |
| III-E Phidget 1044 | None | — |
| III-F Firmware | Toolchain and embedded architecture only. No motion profile, backlash approach or alternatives | `reference/firmware.md` |
| III-G Calibration | Calibration sketch and 830–2170 µs working limits. Table VI constants and compliance correction: none | `reference/servos.md:14-21` |
| III-H Scan software | Host does "scan planning, logging" (diagram only) | PNG |
| III-I, III-J | None | — |
| IV Evaluation (all) | None | — |
| V Conclusion / Future work | Open issues partly overlap: non-magnetic rod ends (skeleton Future Work 3), servo pot feedback (skeleton Future Work 5; the pot tap is already physically done, see §10) | `open-issues.md:6`, `reference/servos.md:11` |
| Appendices A/B | Vault README conventions only | `README.md` |

---

## 10. Superseded values and conflicts

The vault is a 2026-08-26 snapshot. Where the skeleton differs, **check which is current before writing**.

| Item | Vault (2026-08-26) | Skeleton | Note |
|---|---|---|---|
| Base triangle side `sb` | 450 mm (`reference/kinematics.md:8`) | 175 mm (III-B) | Skeleton says "old 450/18/180/600 values are not used anywhere". Superseded. |
| Platform side `sp` | 18 mm (`:9`) | 75 mm | Superseded. 18 mm looks implausible for a ball-joint triangle, but the vault says "Confirmed build parameters". The reason it changed is not recorded. |
| Bicep `L` | 180 mm (`:10`) | 177 mm | Superseded. Bicep notes still say 180 mm centre-to-centre, ~210 mm printed (`reference/mechanical.md:15-16`). Skeleton III-D says 177 mm. |
| Forearm `l` | 600 mm (`:11`) | 625 mm | Superseded. |
| Depth/workspace | 276 mm reachable, 24 mm short, z ∈ [−450, −750] (`:18`) | z −540 to −788 mm; box z −600 to −700 | Superseded; the shortfall item is flagged "removed" in skeleton IV-K. |
| "Wrong" inherited values 567/76/524/1244 | Described as wrong (`:14`) | — | `sources.md` (williams2016delta table, p. 6) lists these as the ABB FlexPicker IRB 360-1/1600 dimensions (s_B 567, s_P 76, L 524, l 1244). So they are a real robot's dimensions, not an error in the upstream author's code. My inference from the sources file; the vault does not say it. |
| Servo supply | 4×AA pack at 6 V (`reference/servos.md:9`) | "6 V bench supply" (III-E) | Conflict. One is the later setup; not recorded which. |
| Servo feedback | Pot already tapped with wires; closed-loop `moveTo` in bring-up plan (`reference/servos.md:11-12`, `:27`) | Pot feedback "deferred"; open-loop final (III-G, V) | The skeleton rationale ("pot sits on the output shaft") is not in the vault. |
| Magnetometer data path | `DATA a b c bx by bz` returns through the Arduino over serial (diagram) | Magnetometer is a Phidget 1044 on its own USB link to the host, bypassing the Arduino (III-A) | Direct conflict. The skeleton gives the reason (no signal wiring down the arms, field data off the control link); the vault does not. |
| IK location | Host does "IK" (diagram) | Arduino "only solves the kinematics" (III-A) | Conflict. |
| Serial protocol | Line-based ASCII `MOVE a b c` (diagram) | Mode byte + JSON in the upstream GUI format [9] (III-A) | Conflict. |
| Servo library | `VarSpeedServoRA4M1` (diagram); `Servo` library with EEPROM (`reference/servos.md:19`) | Not specified; motion profile is smoothstep with T = max(...) (III-F) | Conflict or later change; not recorded. |
| Servo limits | 800–2200 µs hard; ~830–2170 µs working (`reference/servos.md:14-15`) | 830–2170 µs clamp (III-E) | Consistent. |
| Top plate | 6 mm acrylic → 6 mm aluminium (`reference/mechanical.md:6`) | "acrylic prototype, aluminium final [CHECK: which is fitted]" | The vault gives no answer. |
| Rod-end supplier | "Small Parts & Bearings" (`reference/bom-materials.md:18`) | NZ supplier, NZ$6.90 + GST [25] | Check which supplier was actually used. |
| Rod-end status | "prototype only", swap planned (`reference/rod-ends-joints.md:6`) | Final design still uses steel balls, "partly met" (R1) | Skeleton: no non-magnetic rod end was available in time. Consistent as a trajectory. |
| Servo count / alternates | Adafruit shield in BOM but unused (`reference/servos.md:8`) | No shield in design | Consistent; the shield should probably be dropped from Table V. |

**Internal vault inconsistencies.**
- `reference/mechanical.md:15-16` gives the bicep as ~210 mm printed / 180 mm pivot-to-pivot, and `reference/kinematics.md:10` says `L` = 180 mm, so those two agree with each other.
- The 750 mm stand triangle (`reference/mechanical.md:26`) is 433 mm circumradius. That checks (750/√3 ≈ 433, my arithmetic), but the 750 mm side differs from `sb` = 450 mm, which is the base triangle through the servo shafts, not the stand. They are different things; don't mix them.

---

## 11. What to fetch elsewhere

Most of the skeleton's evidence is not here. To fill the gaps you will need:
1. The firmware/analysis repo (`engr489-firmware/`, `reference/firmware.md:5`) and the GitLab repo in Appendix A, for code, tests, Table VI constants and the correction coefficients.
2. Lab data and plots, for all of Section IV and Figs. 2–14.
3. A fresh "update the vault" pass, if you want this repo to be the single record. The vault was set up on 2026-08-26 and has not been updated since (one commit, one worklog entry).
