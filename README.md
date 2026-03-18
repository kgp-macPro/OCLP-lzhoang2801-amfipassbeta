<div align="center">
<img src="docs/images/OC-Patcher.png" alt="OpenCore Patcher Logo" width="256" />
<h1>Preserved Tahoe Patchset Reference (OCLP 3.0.0 Nightly state)</h1>
</div>

This repository contains a preserved working state of the Tahoe patchset as it existed in the final lzhoang2801 OCLP 3.0.0 Nightly snapshot (Dec 24, 2025), which is no longer directly reproducible under macOS Tahoe due to missing resources (AppleHDA) in the referenced PatcherSupportPkg.

In the Dec 24, 2025 snapshot, the last upstream commit references Universal-Binaries from an upstream PatcherSupportPkg source whose distributed Universal-Binaries package does not include AppleHDA.
As a result, the modern audio (AppleHDA) root patch cannot be applied from that snapshot without providing a Universal-Binaries package that contains AppleHDA.

This repository restores a working state by redirecting the Universal-Binaries download to a preserved mirror that includes AppleHDA (and thus matches the intended Tahoe patchset requirements). No new patches are introduced; only the original resource location was restored.

This fork is **not an official upstream release** of OpenCore Legacy Patcher and is not affiliated with the Dortania OCLP project.

This fork aims to restore modern Wi-Fi (including AirDrop and AirPlay) and modern audio (AppleHDA) on advanced Hackintosh systems running macOS Tahoe 26.x. Do **not** apply root patches on unsupported native Macs or on Hackintosh systems with unsupported hardware (e.g. GPUs). Apart from modern Wi-Fi and modern audio, other root patches are expected to fail.

This fork is not an official OCLP project and is provided for documentation and testing purposes only. It reflects development work originally performed by the OCLP contributors.

This fork is intended for testing the historical Tahoe patchset behavior with regard to modern Wi-Fi and modern audio functionality.

This repository represents a preserved reference implementation of the original Tahoe patchset workflow and is not an actively developed continuation of the patcher.

Active development of the Tahoe patchset continues in the OpenCore Legacy Patcher branch maintained by YBronst (MakAsrock):
https://github.com/YBronst/OpenCore-Legacy-Patcher/releases

---

## AMFI / Signing notice

The distributed binaries are unsigned. Therefore they cannot be used together with **AMFIPass.kext** unless the boot argument `amfi=0x80` is used.

AMFIPass normally requires a properly signed OCLP release. Until an official signed release of OCLP 3.0.0 becomes available, you can enable or disable AMFIPass.kext, but you must use the boot argument:

`amfi=0x80`

With `amfi=0x80`, some applications (for example Firefox) may fail to start.  
To mitigate this behavior, additionally use:

`ipc_control_port_options=0`

(credits to badbrain)

---

## Important dependency

Root patching requires **PatcherSupportPkg** resources provided by this preserved mirror:

https://github.com/kgp-macPro/PatcherSupportPkg-lzhoang2801

If this repository becomes unavailable or private, required downloads will fail.

---

## What was changed here

- Redirected PatcherSupportPkg downloads to the preserved mirror containing the full Universal-Binaries.dmg (including AppleHDA)
- No root patch logic was modified

---

## Important compatibility notice

Early reports suggested that macOS Tahoe 26.4 introduced fundamental changes to the system patching workflow related to HFS+ based patch images.  
Further testing has shown that this assumption was incorrect.

The issues observed in **macOS 26.4 beta 1** were most likely caused by a temporary **HFS+ mounting bug**, which Apple already fixed in **beta 2**.

The remaining problems encountered during root patching were caused by the absence of a **matching Kernel Debug Kit (KDK)**.  
The required KDK was not released until **macOS 26.4 beta 4**.

With **macOS 26.4 beta 4 and the corresponding KDK installed**, root patching works again with the following patcher versions:

- **OCLP 3.0.0 Nightly**
- **OCLP-Mod 3.1.5**
- **OCLP 3.1.6 Nightly**

All three patchers can successfully apply the modern Wi-Fi and modern audio (AppleHDA) root patches when the matching KDK is available.

Booting works with:

`amfi=0x80`

with **AMFIPass.kext either enabled or disabled**. OCLP-Mod 3.1.5 also works with `-amfipassbeta` instead of `amfi=0x80`. 

---

This repository serves as a stable reference environment for macOS Tahoe 26.0–26.4 systems requiring fully working modern Wi-Fi and AppleHDA audio.

Active development of the Tahoe patchset continues in the OpenCore Legacy Patcher branch maintained by YBronst (MakAsrock):
https://github.com/YBronst/OpenCore-Legacy-Patcher/releases

---

## Setup Guidelines and Community Discussion

Detailed setup instructions, prerequisites, troubleshooting tips and ongoing discussion can be found in the following threads:

**InsanelyMac:**  
https://www.insanelymac.com/forum/topic/362042-experimental-fork-of-oclp-300-nightly-%E2%80%93-wi-fi-airdropairplay-and-applehda-fully-working-under-tahoe/

**tonymacx86:**  
https://www.tonymacx86.com/threads/experimental-fork-of-oclp-3-0-0-nightly-wi-fi-airdrop-airplay-and-applehda-fully-working-under-tahoe.332849/

---

## Credits

* [Acidanthera](https://github.com/Acidanthera)
  * OpenCorePkg, as well as many of the core kexts and tools
* [DhinakG](https://github.com/DhinakG)
  * Main co-author
* [Khronokernel](https://github.com/Khronokernel)
  * Main co-author
* [Ausdauersportler](https://github.com/Ausdauersportler)
  * iMacs Metal GPUs Upgrade Patch set and documentation
  * Great amounts of help with debugging, and code suggestions
* [vit9696](https://github.com/vit9696)
  * Endless amount of help troubleshooting, determining fixes and writing patches
* [EduCovas](https://github.com/covasedu)
  * [non-Metal patch set](https://github.com/moraea/non-metal-frameworks) for nVidia Tesla/Fermi/Maxwell/Pascal, AMD TeraScale 1/2, and Intel Core 1st/2nd Generation GPUs
  * [3802 Metal patch set](https://github.com/moraea/misc-patches/tree/main/3802-Metal-15) and [MetallibSupportPkg](https://github.com/dortania/MetallibSupportPkg) for nVidia Kepler and Intel Core 3rd/4th Generation GPUs
  * Metal bundle patches and shims for [nVidia Kepler](https://github.com/moraea/misc-patches/tree/main/Kepler%2013%2B), [AMD GCN 1 - 4](https://github.com/moraea/misc-patches/tree/main/GCN%2013%2B), and [AMD GCN 5 (Vega)](https://github.com/moraea/misc-patches/tree/main/vega%2013%2B)
  * [IOSurface offset patches](https://github.com/moraea/misc-patches/tree/main/Sonoma%2014.4%20IOSurface) for nVidia Kepler, AMD GCN 1 - 5, and Intel Core 3rd - 6th Generation GPUs
  * [legacy Wi-Fi patch set](https://github.com/moraea/unsupported-wifi-patches) restores functionality for Wi-Fi cards in all 2007 - 2017 models
  * [T1 patch set](https://github.com/moraea/misc-patches/tree/main/T1-Patch) restores Touch ID, Apple Pay, and other secure functionality in 2016 - 2017 models
  * AppleGVA downgrade for accelerated video decoding on 2012 - 2016 models
  * OpenCL and OpenGL downgrade for AMD GCN
  * [USB 1 patch](https://github.com/moraea/misc-patches/tree/main/IOUSBHostFamily-14.4)
* [ASentientHedgehog](https://github.com/moosethegoose2213)
  * [non-Metal patch set](https://github.com/moraea/non-metal-frameworks) for nVidia Tesla/Fermi/Maxwell/Pascal, AMD TeraScale 1/2, and Intel Core 1st/2nd Generation GPUs
* [ASentientBot](https://github.com/ASentientBot)
  * [non-Metal patch set](https://github.com/moraea/non-metal-frameworks) for nVidia Tesla/Fermi/Maxwell/Pascal, AMD TeraScale 1/2, and Intel Core 1st/2nd Generation GPUs
  * [Metal bundle interposer](https://github.com/moraea/misc-patches/tree/main/sequoia%2031001%20interposer) for AMD GCN 1 - 5 and Intel Core 5th/6th Generation GPUs
  * [dsce](https://github.com/moraea/dsce) and [shared code](https://github.com/moraea/moraea-common) used by some other patches
* [cdf](https://github.com/cdf)
  * Mac Pro on OpenCore Patch set and documentation
  * [Innie](https://github.com/cdf/Innie) and [NightShiftEnabler](https://github.com/cdf/NightShiftEnabler)
* [Syncretic](https://forums.macrumors.com/members/syncretic.1173816/)
  * [AAAMouSSE](https://forums.macrumors.com/threads/mp3-1-others-sse-4-2-emulation-to-enable-amd-metal-driver.2206682/), [telemetrap](https://forums.macrumors.com/threads/mp3-1-others-sse-4-2-emulation-to-enable-amd-metal-driver.2206682/post-28447707) and [SurPlus](https://github.com/reenigneorcim/SurPlus)
* [dosdude1](https://github.com/dosdude1)
  * Main author of the [original GUI](https://github.com/dortania/OCLP-GUI)
  * Development of previous patchers, laying out much of what needs to be patched
* [parrotgeek1](https://github.com/parrotgeek1)
  * [VMM Patch Set](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/4a8f61a01da72b38a4b2250386cc4b497a31a839/payloads/Config/config.plist#L1222-L1281)
* [BarryKN](https://github.com/BarryKN)
  * Development of previous patchers, laying out much of what needs to be patched
* [mario_bros_tech](https://github.com/mariobrostech) and the rest of the Unsupported Mac Discord
  * Catalyst that started OpenCore Legacy Patcher
* [arter97](https://github.com/arter97/)
  * [SimpleMSR](https://github.com/arter97/SimpleMSR/) to disable firmware throttling in Nehalem+ MacBooks without batteries
* [Mr.Macintosh](https://mrmacintosh.com)
  * Endless hours helping architect and troubleshoot many portions of the project
* [flagers](https://github.com/flagersgit)
  * Aid with Nvidia Web Driver research and development
  * [non-Metal patch set](https://github.com/moraea/non-metal-frameworks) for nVidia Tesla/Fermi/Maxwell/Pascal, AMD TeraScale 1/2, and Intel Core 1st/2nd Generation GPUs
  * [Metal bundle interposer](https://github.com/moraea/misc-patches/tree/main/sequoia%2031001%20interposer) for AMD GCN 1 - 5 and Intel Core 5th/6th Generation GPUs
  * LegacyRVPL, SnapshotIsKill, etc. to aid in rapid testing and development
* [joevt](https://github.com/joevt)
  * [FixPCIeLinkrate](https://github.com/joevt/joevtApps)
* [Jazzzny](https://github.com/Jazzzny)
  * Research and various contributions to the project
  * UEFI Legacy XHCI research and development
  * NVIDIA OpenCL research and development
  * `MacBook5,2` research and development
    * LegacyKeyboardInjector
  * Pre-Ivy Bridge Aquantia Ethernet Patch
  * Non-Metal Photo Booth Patch for Monterey+
  * GUI and Backend Development
    * Updater UI
    * macOS Downloader UI
    * Downloader UI
    * USB Top Case probing
    * Developer root patching
  * Vaulting implementation
  * macOS 15 3802 Helios Research
  * UEFI bootx64.efi research
  * universal2 build research
  * Various documentation contributions
* Amazing users who've graciously donate hardware:
  * [JohnD](https://forums.macrumors.com/members/johnd.53633/) - 2013 Mac Pro
  * [SpiGAndromeda](https://github.com/SpiGAndromeda) - AMD Vega 64
  * [turbomacs](https://github.com/turbomacs) - 2014 5k iMac
  * [vinaypundith](https://forums.macrumors.com/members/vinaypundith.1212357/) - MacBook7,1
   * [ThatStella7922](https://github.com/ThatStella7922) - 2017 13" MacBook Pro (A1708)
  * zephar - 2008 Mac Pro
  * jazo97 - 2011 15" MacBook Pro
  * And others (reach out if we forgot you!)
* MacRumors and Unsupported Mac Communities
  * Endless testing and reporting issues
* Apple
  * for macOS and many of the kexts, frameworks and other binaries we reimplemented into newer ones

## Maintainer
This preservation repository is maintained by **kgp**.
Online identities:
- GitHub: https://github.com/kgp-macPro
- InsanelyMac: kgp-iMacPro
- tonymacx86: kgp

## Disclaimer
This is **not an official Dortania release** and is intended for complex Hackintosh configurations.

**Thanks to:**
* Dortania OCLP team
* lzhoang2801
* YBronst (MakAsrock)
* All PatcherSupportPkg contributors

---
