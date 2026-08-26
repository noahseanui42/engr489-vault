# assets/

Binaries live here — **not** committed to git (git handles them badly).

- CAD (SolidWorks parts/assemblies), STL exports, DXF
- Print photos, bench photos
- Datasheets (servo, magnetometer, rod ends)

Keep this folder cloud-synced (OneDrive via VUW Microsoft 365, or similar). Reference
files by **name** from your notes, e.g. "see top-plate-v3.dxf", rather than pasting them
into markdown. Use ISO dates or version tags in filenames: `top-plate_2026-08-26.dxf`.

Suggested `.gitignore` entry at repo root:

    assets/*
    !assets/README.md
