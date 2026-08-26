# Servos

Current state. Overwrite as things change; log changes in [[worklog]].

**Hardware:** 3× Futaba S3306MG.

**Control (current):** PWM direct off Arduino pins **D9 / D10 / D11** — *no servo shield*.
(The Adafruit 16-ch shield is still in the [[bom-materials|BOM]] but unused for bring-up.)
Power: **6V 4×AA pack**, shared ground with the Arduino.

**Feedback mod:** internal pot tapped with feedback wires. Wiper reads 0.8 V @ 800 µs
and 2.23 V @ 2200 µs — safe straight into A0, no divider needed.

**Travel limits:** 800–2200 µs (1400 µs span, symmetric about 1500 µs). Working
calibrated limits ~830–2170 µs.

## Calibration sketch — `servo_calibration_v3.ino`
- D9, Servo lib + EEPROM storage
- Linear fit `angle = a·counts + b` (counts vs protractor)
- Serial @ 115200, newline; commands `u / a / + / - / [ / ] / c / s / p / w / r`
- Hard limits 800–2200 µs; A0 pot feedback (0.8–2.23 V)

## Bring-up plan (Phases 0–4, exit criteria D1–D6)
1. Open-loop sweep
2. Feedback read
3. Linear calibration vs protractor
4. Closed-loop `moveTo` with proportional pulse trim

`delay()` blocking is fine for one servo — **rework to `millis()` before scaling to 3.** → [[open-issues]]

Related: [[kinematics]], [[firmware]]
