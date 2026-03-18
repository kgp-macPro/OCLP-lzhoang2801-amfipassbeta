<div align="center">
<img src="docs/images/OC-Patcher.png" alt="OpenCore Patcher Logo" width="256" />
<h1>OCLP 3.0.0 (lzhoang2801) – amfipassbeta Variant for macOS Tahoe</h1>
</div>

This repository provides a preserved and adapted version of the final **OCLP 3.0.0 Nightly snapshot (Dec 24, 2025)** by lzhoang2801, specifically configured to work with modern macOS Tahoe systems using the `-amfipassbeta` boot argument.

---

## Overview

The original snapshot is no longer directly usable on macOS Tahoe due to incomplete PatcherSupportPkg resources (notably missing AppleHDA).

This repository restores full functionality by redirecting the PatcherSupportPkg download to a preserved and fixed version that includes complete Universal-Binaries.

No root patch logic has been modified.

---

## Key Features

- Based on original OCLP 3.0.0 (lzhoang2801 snapshot)
- Fully compatible with `-amfipassbeta`
- Restored **AppleHDA (modern audio)** support
- Fully working **modern Wi-Fi stack**
- Complete **AWDL functionality**:
  - AirDrop (bidirectional)
  - AirPlay
  - Screen Mirroring
  - Handoff / Continuity
- No dependency on `amfi=0x80`

---

## Requirements

- Boot argument:

-amfipassbeta


- Compatible system capable of running Tahoe root patches

---

## PatcherSupportPkg Dependency

This repository relies on the following preserved PatcherSupportPkg:

https://github.com/kgp-macPro/PatcherSupportPkg-laobamac

It provides the required Universal-Binaries including AppleHDA for Tahoe.

---

## Tested Configuration

Fully verified on:

- macOS 26.4 beta 4

Working components:

- AppleHDA (audio)
- Wi-Fi
- AirDrop (bidirectional)
- AirPlay / Screen Mirroring
- Handoff / Continuity

---

## Important Notes

- This is **not an official Dortania OCLP release**
- This is a **preserved and adapted reference implementation**
- Only the PatcherSupportPkg source has been changed
- No additional patch logic has been introduced

---

## Purpose

This repository serves as a **stable reference environment** for:

- macOS Tahoe 26.x
- modern Wi-Fi (AWDL)
- modern audio (AppleHDA)
- amfipassbeta-based patching workflows

---

## Community & Discussion

Further discussion and setup details:

**InsanelyMac:**  
https://www.insanelymac.com/forum/topic/362042-experimental-fork-of-oclp-300-nightly-%E2%80%93-wi-fi-airdropairplay-and-applehda-fully-working-under-tahoe/

**tonymacx86:**  
https://www.tonymacx86.com/threads/experimental-fork-of-oclp-3-0-0-nightly-wi-fi-airdrop-airplay-and-applehda-fully-working-under-tahoe.332849/

---

## Credits

All credits go to the original OCLP developers and contributors.

This repository only preserves and restores functionality:

- Dortania OCLP Team  
- lzhoang2801  
- All PatcherSupportPkg contributors  

---

## Maintainer

Maintained by **kgp**

- GitHub: https://github.com/kgp-macPro  
- InsanelyMac: kgp-iMacPro  
- tonymacx86: kgp  

---

## Disclaimer

This is an experimental preservation setup intended for advanced Hackintosh environments.

Use at your own risk.