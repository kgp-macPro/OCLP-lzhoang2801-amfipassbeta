<div align="center">
<img src="docs/images/OC-Patcher.png" alt="OpenCore Patcher Logo" width="256" />
<h1>OCLP 3.0.0 Nightly – amfipassbeta Variant for macOS Tahoe (based on lzhoang2801)</h1>
</div>

---

## Recommended Setup

This repository provides the **recommended way** to run the preserved OCLP 3.0.0 Tahoe patchset using:

**AMFIPass.kext + boot argument `-amfipassbeta`**

Unlike the original setup, this variant **does not require `amfi=0x80`**, avoiding application compatibility issues.

For full documentation, compatibility details and updates, see:

**InsanelyMac thread (primary reference):**  
https://www.insanelymac.com/forum/topic/362042-experimental-fork-of-oclp-300-nightly-%E2%80%93-modern-wi-fi-awdl-and-applehda-fully-working-under-tahoe/

---

## Overview

This repository provides a preserved and adapted version of the final **OCLP 3.0.0 Nightly snapshot (Dec 24, 2025)** by lzhoang2801, configured for macOS Tahoe 26.x.

The original snapshot is no longer directly usable on Tahoe due to incomplete PatcherSupportPkg resources (missing AppleHDA).

This repository restores full functionality by redirecting the PatcherSupportPkg download to a preserved version including complete Universal-Binaries.

**No root patch logic has been modified.**

---

## Functionality

The following components are confirmed working with this setup:

- modern audio (AppleHDA)  
- modern Wi-Fi (Broadcom and supported Intel chipsets)  

AWDL stack:
- AirDrop (bidirectional)  
- AirPlay  
- Screen Mirroring  

Continuity:
- Handoff (e.g. Mail, Notes, Safari)  
- Sidecar (currently not functional)  

---

## Requirements

- Boot argument:  
  `-amfipassbeta`

- A suitable **Kernel Debug Kit (KDK)** is required for OCLP root patching  

For compatibility details (macOS versions and KDK handling), see the thread.

---

## PatcherSupportPkg Dependency

This repository relies on:

https://github.com/kgp-macPro/PatcherSupportPkg-laobamac

Provides required Universal-Binaries including AppleHDA for Tahoe.

---

## Repository Scope

This repository:

- does **not introduce new patch logic**  
- restores a reproducible working state of the original snapshot  
- redirects PatcherSupportPkg to a preserved version including AppleHDA  

---

## Important Notes

- this fork is **not supported by the OCLP developers**  
- intended for **advanced Hackintosh configurations only**  
- no patches other than modern audio (AppleHDA) and modern Wi-Fi + AWDL are expected to work  
- always keep a bootable backup before applying root patches  

---

## Community & Discussion

Additional discussion:

**tonymacx86 (mirror thread):**  
https://www.tonymacx86.com/threads/experimental-fork-of-oclp-3-0-0-nightly-modern-wi-fi-awdl-and-applehda-fully-working-under-tahoe-26-x.332849/

---

## Credits

- Dortania OCLP Team  
- lzhoang2801  
- laobamac_yyds  
- InsanelyMac community  
- tonymacx86 community (mirror thread)

---

## Maintainer

Maintained by **kgp**

- GitHub: https://github.com/kgp-macPro  
- InsanelyMac: kgp (formerly KGP-iMacPro)  
- tonymacx86: kgp  

---

## Disclaimer

This is an experimental preservation setup intended for advanced Hackintosh environments.

Use at your own risk.