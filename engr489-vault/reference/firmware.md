# Firmware / Software

Current state. Overwrite as things change; log changes in [[worklog]].

- **Repo:** `engr489-firmware/` parent with firmware subdirectories. Uploaded, README drafted.
- **MATLAB/Simulink:** kinematics codebase cleaned up (duplicate functions resolved,
  parameter mismatch fixed — see [[kinematics]] gotcha).
- **ADC:** 12-bit sufficient; using 14-bit for noise-averaging headroom.
- **Embedded architecture (RA4M1):** USB CDC serial, GPT timers for PWM, peripheral
  clock tree 48 MHz HOCO → PCLKD / PCLKB / USBFS.
- **Toolchain gotcha:** `LIBUSB_ERROR_TIMEOUT` DFU on the lab machine — needs WinUSB
  driver via Zadig, blocked by admin rights. Sort *before* a lab session. → [[open-issues]]

Related: [[servos]]
