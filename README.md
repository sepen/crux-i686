# CRUX-i686

**Reviving CRUX for legacy 32-bit systems**

This project provides a **root filesystem image** and a set of **port overlays** that bring back **i686 (32-bit x86)** support to the minimalist [CRUX Linux](https://crux.nu) distribution.  
It is intended for hobbyists, retrocomputing enthusiasts, and anyone who still has reliable old hardware capable of running a lightweight and source-based Linux system.

**Download the root filesystem:**  
[crux-i686-3.8-rootfs.tar.xz](https://github.com/sepen/crux-i686/releases/download/3.8/crux-3.8-i686-rootfs.tar.xz)


---


## Overview

CRUX officially targets the **x86-64** architecture, and official 32-bit support was dropped after version **3.5**.  
The **CRUX-i686** project reintroduces a functional i686 environment based on **CRUX 3.8**, marking the **first unofficial i686 release since CRUX 3.5**.

This release includes:

- A prebuilt root filesystem:  
  **`crux-i686-3.8-rootfs.tar.xz`** – a minimal CRUX 3.8 base system bootable on i686 CPUs.
- Architecture-specific port overlays:
  - [core-i686](https://github.com/sepen/crux-ports-core-i686) — base system ports adapted for i686  
  - [opt-i686](https://github.com/sepen/crux-ports-opt-i686) — optional and userland software ports  
  - [xorg-i686](https://github.com/sepen/crux-ports-xorg-i686) — X.Org and graphical environment ports  

These overlays contain adjusted `Pkgfile`s and build options tuned for the i686 instruction set and older toolchains.  
They come **preinstalled and preconfigured** in the `crux-i686-3.8-rootfs.tar.xz` image.


---


## Target Audience

- Legacy PCs and laptops (Pentium III, Pentium M, early Atom, VIA C3, etc.)
- Retro or embedded x86 systems
- Users who prefer source-based, minimal Linux systems

CRUX-i686 aims to stay close to the upstream CRUX philosophy — *simple, transparent, and minimal* — while keeping older hardware usable.


---


## Installation

### 1. Prepare the environment

You can deploy CRUX-i686 in a VM, chroot, or directly on hardware that supports i686.

Example (for a chroot or disk install):

```shell
curl -O https://example.com/crux-i686-3.8-rootfs.tar.xz
sudo tar xpvf crux-i686-3.8-rootfs.tar.xz -C /mnt
sudo mount -t proc /proc /mnt/proc
sudo mount --rbind /sys /mnt/sys
sudo mount --rbind /dev /mnt/dev
sudo chroot /mnt /bin/bash
```

### 2. Configure port collections

Edit `/etc/prt-get.conf` and add the i686 overlays before the default collections so that they take precedence:

```shell
prtdir /usr/ports/core-i686
prtdir /usr/ports/opt-i686
prtdir /usr/ports/xorg-i686
prtdir /usr/ports/core
prtdir /usr/ports/opt
prtdir /usr/ports/xorg
```

Then sync and update:
```shell
ports -u
prt-get sysup
```

### 3. Build and install software

Use the regular CRUX tools (prt-get, pkgmk, etc.) to build packages.
The overlays ensure proper compiler flags and dependencies for 32-bit systems.

Example:
```
prt-get update -fr gcc
```


## Notes on compatibility

- This CRUX-i686 3.8 release is unofficial — not supported by the CRUX core team.
- It is the first community-maintained i686 release since CRUX 3.5.
- Some modern packages may fail to build due to upstream dropping i686 support.
- When no port exists in an i686 overlay, the default (x86-64) port is used as fallback — manual fixes may be required.
- Use at your own risk; feedback and patches are welcome.


---


## Philosophy

> “Keep it simple.” — CRUX motto

CRUX-i686 follows the same ideals as upstream CRUX:
- No unnecessary patches
- Transparent build process
- Easy to understand and maintain system layout
This project’s only deviation is architecture support, not philosophy.


---


## License

All CRUX base ports remain under their respective upstream licenses.
Overlay modifications and scripts are released under the MIT License.


---


## Credits

- [CRUX Linux Team](https://crux.nu/)
- [CRUX-ARM project](https://crux-arm.nu/) — inspiration for overlay design
- Community maintainers and retro-hardware enthusiasts
