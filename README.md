<div align="center">
<img src="docs/images/OC-Patcher.png" alt="OpenCore Patcher Logo" width="256" />
<h1>OCLP 3.0.0 Nightly – amfipassbeta Edition for macOS Tahoe</h1>
</div>

---

## Established Conservative Setup

This repository provides the **established, extensively tested conservative AMFIPass-based edition** of the preserved OCLP 3.0.0 Tahoe patch environment using:

**AMFIPass.kext + boot argument `-amfipassbeta`**

Unlike the original setup, this variant **does not require `amfi=0x80`**, avoiding application compatibility issues.

For full documentation, compatibility details, proper setup and EFI configuration, see:

**InsanelyMac thread (primary reference):**  
https://www.insanelymac.com/forum/topic/362042-experimental-fork-of-oclp-300-nightly-%E2%80%93-modern-wi-fi-awdl-and-applehda-fully-working-under-tahoe/

---

## Three Established Tahoe Approaches

OCLP-CustoMac does not obsolete or withdraw the two earlier KGP Tahoe configurations. All three approaches remain intentionally available.

### 1. OCLP 3.0.0 Nightly – Preserved Reference Edition

Repository: [kgp-macPro/OCLP-lzhoang2801](https://github.com/kgp-macPro/OCLP-lzhoang2801)

- conservative reference environment closest to the earlier working lzhoang2801 OCLP 3.0.0 Nightly Tahoe state;
- uses the earlier working lzhoang2801 PatcherSupportPkg containing Modern Wireless resources and AppleHDA;
- retains the historical `amfi=0x80` and `ipc_control_port_options=0` AMFI path;
- preserved for users who value maximum proximity to the original Nightly architecture.

### 2. OCLP 3.0.0 Nightly – amfipassbeta Edition

Repository: [kgp-macPro/OCLP-lzhoang2801-amfipassbeta](https://github.com/kgp-macPro/OCLP-lzhoang2801-amfipassbeta)

- conservative and extensively tested on real systems over many months;
- remains close to the preserved Nightly architecture;
- uses `AMFIPass.kext + -amfipassbeta`;
- its documented Intel configuration uses a Broadcom `IOName` spoof with AirportItlwm;
- remains fully available; satisfied users do not need to migrate, and migration is optional.

### 3. OCLP-CustoMac

Repository: [kgp-macPro/OCLP-CustoMac](https://github.com/kgp-macPro/OCLP-CustoMac)

Release: [OCLP-CustoMac 3.0.0](https://github.com/kgp-macPro/OCLP-CustoMac/releases/tag/v3.0.0)

- current recommended KGP setup for new installations and users who want the further-developed patcher architecture;
- further-developed focused branch with direct Intel detection;
- does not require a Broadcom `IOName` spoof for Intel detection;
- selectable Modern Wi-Fi and Modern Audio;
- automatic and optional manual KDK selection;
- strengthened root-patch recovery;
- APFS internal resources;
- reproducible, validated builds.

---

## Overview

This repository provides a reproducible and adapted version of the final OCLP 3.0.0 Nightly snapshot (Dec 24, 2025) by lzhoang2801, configured for macOS Tahoe 26.x.

The original snapshot is no longer directly usable on Tahoe due to incomplete PatcherSupportPkg resources.

This repository restores the functionality required for modern AppleHDA, Wi-Fi and AWDL support by using a compatible PatcherSupportPkg providing complete Universal-Binaries and enabling compatibility with AMFIPass.kext and `-amfipassbeta`.

No original Tahoe root patch logic has been modified.

---

## Scope Clarification

This repository is intended exclusively for advanced Hackintosh systems running macOS Tahoe 26.x.

It is NOT a general unsupported-Mac patching project.

No additional graphics acceleration patches or unsupported-Mac root patch frameworks are included.

This repository intentionally remains as close as possible to the original OCLP 3.0.0 Nightly Tahoe baseline released by the OCLP developers and later preserved by lzhoang2801.

The fork only enables and preserves the original Tahoe patch functionality already implemented by the OCLP developers.

---

## Functionality

### Modern Audio / AppleHDA

- modern audio (AppleHDA)

### Broadcom Modern Wireless

The validated Broadcom path includes:

- Wi-Fi
- AirDrop (bidirectional)
- AirPlay (bidirectional)
- Screen Mirroring (bidirectional)
- Personal Hotspot
- Continuity Camera
- Handoff (e.g. Mail, Notes, Safari)

### Intel Wi-Fi

Intel Wi-Fi operation depends on external AirportItlwm. This amfipassbeta Edition retains the historically documented Broadcom `IOName` spoof used for Intel detection; existing users should not remove that spoof merely because OCLP-CustoMac uses a different detector, and it is not obsolete for this edition.

OCLP-CustoMac differs by detecting Intel hardware directly from its authentic PCI identity and therefore does not require Broadcom `IOName` spoofing for OCLP-CustoMac itself.

Current AirportItlwm does not provide the complete native AWDL control/data path required for reliable bidirectional AirDrop, Personal Hotspot or Continuity Camera. Intel therefore does not inherit the complete Broadcom AWDL/Continuity claim above.

### Sidecar

- currently not functional

---

## Requirements

- Boot argument:  
  `-amfipassbeta`

- A suitable **Kernel Debug Kit (KDK)** is required for OCLP root patching

For compatibility details (macOS versions and KDK handling), see the InsanelyMac thread or its mirror on tonymacx86.

---

## PatcherSupportPkg Dependency

This repository relies on:

https://github.com/kgp-macPro/PatcherSupportPkg-laobamac

This PatcherSupportPkg provides complete Universal-Binaries and enables compatibility with AMFIPass.kext and `-amfipassbeta`.

OCLP-CustoMac retains the same KGP-maintained signed PatcherSupportPkg payload lineage used by the amfipassbeta Edition while implementing its own separate patcher-control architecture.

### Verified Payload Relationship

The PatcherSupportPkg history requires an important distinction.

The final published OCLP 3.0.0 Nightly release by lzhoang2801 references a newer PatcherSupportPkg that no longer contains the required Tahoe `AppleHDA.kext`. As a result, root patching with that currently published configuration fails because the expected AppleHDA payload cannot be found.

The separately preserved edition corrects this by redirecting OCLP to an earlier lzhoang2801 PatcherSupportPkg that still contains the required `AppleHDA.kext`.

This amfipassbeta edition instead uses a KGP-maintained derivative of laobamac's PatcherSupportPkg. Because laobamac's original package also did not contain the required Tahoe `AppleHDA.kext`, that payload was restored unchanged by KGP from the earlier working lzhoang2801 PatcherSupportPkg.

An offline comparison of all resources actually consumed by the enabled `Modern Wireless` and `Modern Audio` patchsets confirmed:

- `wifip2pd` is byte-identical in the earlier lzhoang2801 package and the KGP-maintained laobamac derivative.
- The restored `AppleHDA.kext` is byte-identical to the payload from the earlier working lzhoang2801 PatcherSupportPkg.
- Five Modern Wireless framework executables have identical architectures, paths, permissions and executable `__text` sections:
  - `IO80211`
  - `IO80211Old.dylib`
  - `LibSystemShim.dylib`
  - `WiFiPeerToPeer`
  - `WiFiPeerToPeerOld.dylib`
- The relevant difference in these five files is their embedded code-signature and associated link-edit metadata.
- The earlier lzhoang2801 variants are ad-hoc signed.
- The laobamac variants contain non-ad-hoc embedded signatures.

The PatcherSupportPkg redirect does not modify OCLP's Modern Wireless or Modern Audio patch definitions, destination paths, APFS snapshot handling, kernel-cache rebuilding, root-patch application logic or root-patch reversion logic.

This comparison refers specifically to the earlier working lzhoang2801 PatcherSupportPkg deliberately used by the preserved edition. It does not describe or make assumptions about the newer incomplete PatcherSupportPkg referenced by lzhoang2801's final published release.

---

## Repository Scope

This repository:

- provides a reproducible working reference of the original OCLP 3.0.0 Nightly snapshot
- restores the missing Tahoe `AppleHDA.kext` and preserves the resources required for modern Wi-Fi and AWDL functionality
- uses a PatcherSupportPkg compatible with AMFIPass.kext and `-amfipassbeta`, including AppleHDA
- does **not introduce any new patch logic**

---

## Important Notes

- this fork only enables and preserves the original Tahoe patch functionality already implemented by the OCLP developers
- this fork is **not supported by the OCLP developers**
- intended for **advanced Hackintosh configurations only**
- modern audio (AppleHDA) and the validated Broadcom Modern Wireless AWDL/Continuity path are expected to work reliably; Intel remains subject to external AirportItlwm limitations
- no additional graphics acceleration or unsupported-Mac root patch frameworks are included
- always keep a bootable backup before applying root patches

---

## Community & Discussion

Additional discussion:

**tonymacx86 (mirror thread):**  
https://www.tonymacx86.com/threads/experimental-fork-of-oclp-3-0-0-nightly-modern-wi-fi-awdl-and-applehda-fully-working-under-tahoe-26-x.332849/

---

## Credits

- Dortania OCLP Team (original OCLP authors and developers)
- [crystall1nedev](https://github.com/crystall1nedev) (Eva Isabella Luna) (original OCLP 3.0.0 Nightly release)
- [lzhoang2801](https://github.com/lzhoang2801) (original OCLP 3.0.0 Nightly fork)
- [kgp-macPro](https://github.com/kgp-macPro) (preservation, maintenance, AMFIPass integration, AppleHDA restoration, testing and documentation)
- [laobamac](https://github.com/laobamac) (amfipassbeta PatcherSupportPkg)
- [YBronst](https://github.com/YBronst) (OCLP Nightly development)
- badbrain (boot-arg ipc_control_port_options=0 support)
- [zxystd](https://github.com/zxystd) (itlwm/AirportItlwm project)
- [lshbluesky](https://github.com/lshbluesky) (IntelBluetoothFirmware maintenance and releases)
- [Vinhts](https://github.com/Vinhts) (IntelBTPatcher Tahoe 26.5 Bluetooth LE fixes)
- [Z3c0ld](https://github.com/Z3c0ld) (IntelBTPatcher Tahoe 26.5 Bluetooth LE fixes)
- InsanelyMac community
- tonymacx86 community (mirror thread)

For a complete list of OpenCore Legacy Patcher contributors, please refer to the original Dortania repository:

https://github.com/dortania/OpenCore-Legacy-Patcher

---

## Maintainer

Maintained by **kgp**

- GitHub: https://github.com/kgp-macPro
- InsanelyMac: kgp (formerly KGP-iMacPro)
- tonymacx86: kgp

---

## Disclaimer

This repository provides a preserved and maintained Tahoe patch environment intended for advanced Hackintosh systems.

Not intended for unsupported Macs requiring graphics acceleration root patches.

Use at your own risk.

---

If this repository was useful to you:

A coffee is always appreciated ☕  
https://buymeacoffee.com/kgp.macpro