# Redmi 9T (lime) — One UI 8 DSU Research Attempt

**Status: RESEARCH ONLY — NO WORKING IMAGE**

This repository documents an attempt to produce a DSU-sideloadable One UI 8 image for the Xiaomi Redmi 9T (`lime` / M2010J19SG) following the public method used by [Nekover2/OneUI8-Tablet-GSI](https://github.com/Nekover2/OneUI8-Tablet-GSI).

## Explicit failure statements

- **NO GENUINE S25 ULTRA (`pa3q`) ONE UI 8 PORT PRODUCED**
- **NO DSU-BOOTABLE PACKAGE PRODUCED**
- **NO INSTALLABLE ROM PRODUCED**

No `system.img`, no `.img.zst`, no DSU payload, and no claim that anything boots on a real Redmi 9T.

## What is in this repo

| Path | Description |
|------|-------------|
| `REDMI_9T_LIME_ONE_UI_8_FINAL_DELIVERY.md` | Full delivery report, blockers, identity test, environment limits |
| `donor/nekover2_patches/` | Byte-patch scripts copied from Nekover2 (build-specific) |
| `docs/nekover2_*.md` | Nekover2 patching docs, status and manifest for reference |
| `device/` | Sample BoardConfig and init identity fragments for `lime`/`chime` |
| `logs/` | Environment, HTTP headers of the Mystic pa3q donor, etc. |
| `checksums/` | Hashes of the files that were produced |

## Why a ready image was not created

1. Sandbox disk/RAM insufficient to download + unpack a ~5–9 GiB Mystic GSI.
2. Nekover2 patches contain hardcoded offsets for one specific Tab S9 build; they cannot be applied blindly to a `pa3q` or other build.
3. Redmi 9T vendor is Android 12 era (kernel 4.19). Even after framework null-guards, large HAL/VINTF gaps remain.
4. No physical Redmi 9T was available for the iterative DSU + logcat cycle that Nekover2 used.

## How a capable user could continue (Nekover2-style)

See section 17–18 of `REDMI_9T_LIME_ONE_UI_8_FINAL_DELIVERY.md` and Nekover2’s own `docs/patching.md`.

Rough outline:

1. Obtain a Mystic One UI 8 GSI and verify fingerprint.
2. On a Linux machine with root and ≥25 GB free, mount the system image.
3. Re-probe dex offsets for **that exact build**.
4. Adapt the five patch scripts.
5. Apply patches + config fixes, strip AOT artifacts.
6. Deploy via DSU / `gsi_tool` on an unlocked Redmi 9T and iterate with logcat.

Success is not guaranteed because of the vendor generation gap.

## License / legal

- Analysis and scripts in this repo: for documentation and research.
- Nekover2 patch scripts retain their original license (MIT per that project).
- No Samsung, Xiaomi or Qualcomm proprietary binaries are redistributed.
- Mystic GSI itself is an unofficial third-party project; obtain it from its original source if you choose to experiment.

## Credits

- [Nekover2/OneUI8-Tablet-GSI](https://github.com/Nekover2/OneUI8-Tablet-GSI) — the only public, detailed write-up of making a Mystic One UI 8 GSI boot on a non-Samsung device.
- Mystic GSI project — source of the unofficial One UI GSI builds.
- crDroid / community device trees for `chime`/`lime` identity reference.

---

**Do not flash or DSU-sideload anything from this repository expecting a working One UI 8 on Redmi 9T. Nothing bootable is provided.**
