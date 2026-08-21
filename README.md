# Kernel-Lamu Patches

Standalone, portable patches extracted from the
[motorola-lamu-kernel-6.6](https://github.com/OWLXS/motorola-lamu-kernel-6.6) /
[motorola-lamu-device-modules-6.6](https://github.com/OWLXS/motorola-lamu-device-modules-6.6)
project — meant to be easy to port onto other GKI 6.6 (or similarly-shaped)
kernel trees, without needing the whole custom kernel as a base.

These are just the small, self-contained tweaks. The bigger change (swapping
KernelSU-Next for ReSukiSU + integrating SUSFS) isn't here — that's a
387-file change involving a git submodule swap, not something that fits the
"patch" format meaningfully. See the main repos above for that.

## Layout

- `kernel-6.6/` — patches against the ACK/GKI kernel tree
  (`arch/arm64/configs/gki_defconfig`, `drivers/block/zram/zram_drv.c`).
- `kernel_device_modules-6.6/` — patches against the MediaTek device-tree /
  vendor module source (`drivers/misc/mediatek/...`, `build.sh`).
- `ReSukiSU/` — a patch against the KernelSU-fork submodule's own
  `kernel/Kbuild` (applies to KernelSU, KernelSU-Next, ReSukiSU, and similar
  forks alike, not fork-specific).

## Applying

From the root of the tree the patch targets:

```bash
git am path/to/000X-name.patch
# or, if it's not a git repo / you just want the diff applied:
patch -p1 < path/to/000X-name.patch
```

Read each patch's description first — a couple of them mention values you
should double-check/adjust for your own device (touch-boost timing constants
tuned for a specific CPU topology, the ReSukiSU pinned-version fallback
values, etc.) rather than blindly applying as-is.

## Credits

These patches were written for the Kernel-Lamu project — see that repo's
[Credits section](https://github.com/OWLXS/motorola-lamu-kernel-6.6#credits)
for the upstream projects (ReSukiSU, SUSFS, AnyKernel3, LineageOS) this work
builds on top of.
