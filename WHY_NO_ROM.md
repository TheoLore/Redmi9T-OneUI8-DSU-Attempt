# Why there is still no ready One UI 8 ROM for Redmi 9T

You asked to use GitHub Actions to force the creation of the image.

A workflow has been added (`.github/workflows/attempt-gsi.yml`).
It can be triggered manually from the Actions tab.

What it actually does:
- Prints the runner's free disk and RAM.
- Sends a HEAD request to the known Mystic `pa3q` ZIP to confirm size.
- Uploads the HTTP headers as an artifact.
- Prints the same failure statements as the rest of this repository.

What it deliberately does **not** do:
- Download the multi-gigabyte ZIP (runners do not have reliable free space for a full unpack + patch + artifact cycle).
- Mount a system.img and apply byte patches.
- Produce a DSU package.
- Claim that anything boots on Redmi 9T.

## Hard constraints that Actions cannot remove

1. **Image size** – The Mystic One UI packages are several gigabytes compressed and larger when unpacked. GitHub-hosted runners have limited free disk and short job timeouts.
2. **Build-specific patches** – Nekover2's scripts contain hardcoded offsets for one exact Tab S9 build. They abort on any other `services.jar`. Relocating offsets requires the full image and interactive probing.
3. **Vendor gap** – Redmi 9T uses an Android 12-era vendor and kernel 4.19. Even a successfully patched framework GSI is very likely to fail on camera, radio, fingerprint, and other HALs. Fixing those needs repeated DSU boots and logcat on the real phone.
4. **No device** – Without the physical Redmi 9T, there is no way to validate boot or produce the evidence the original request demanded.

## What "success" would actually require

- A machine (or self-hosted runner) with tens of gigabytes free and root.
- The exact GSI build you want to start from.
- Ability to re-probe and adapt the byte patches for that build.
- An unlocked Redmi 9T with a way to run DSU / gsi_tool.
- Multiple iteration cycles of boot → logcat → fix → rebuild.

None of those are available inside a standard GitHub Actions job or the previous sandbox.

## Status (unchanged)

**NO GENUINE S25 ULTRA ONE UI 8 PORT PRODUCED**  
**NO DSU-BOOTABLE PACKAGE PRODUCED**  
**NO INSTALLABLE ROM PRODUCED**

This repository remains research documentation only.
