# IOS-15-USB Historical Archive Audit

## Purpose and status

This repository preserves the **old IOS-15-USB package** as historical forensic reference only. Archive/bootstrap date: **2026-09-25**.

It is **not** current VCAM PRO implementation, **not** iOS 15.8.8 runtime proof, and **not** device validation. No package behavior was changed, no fixes were performed, and no device operation was performed.

## Exact source artifact

- Original filename: `ios 15 usb.deb`
- Byte size: `204590`
- SHA-256: `d85c2736941773d07351d43dd3a5cef98125e1bd31e776564377ee3446a24067`

## Package metadata - OBSERVED

```text
Package: com.vcam.universal
Name: VCam Universal Patch
Version: 1.0.0
Architecture: iphoneos-arm64
Depends: mobilesubstrate
Description: Bypass universal para VCam
```

## Complete extracted-file inventory - OBSERVED

```text
DEBIAN/control
var/jb/Library/MobileSubstrate/DynamicLibraries/VCamRecovered.dylib
var/jb/Library/MobileSubstrate/DynamicLibraries/VCamRecovered.plist
var/jb/var/mobile/Library/Preferences/com.if-she.cydia.vcam.plist
```

The package payload installs the three files under `/var/jb/...`; `DEBIAN/control` is package control metadata retained by the archive extraction.

## Raw ar members - OBSERVED

- `control.tar.gz` - de5b2185a7ede1c9e233f4320704820e7dbe31acb019e6846a390ae18eb0d1de
- `data.tar.gz` - 70c79ce323ff69a8a8a57104d28e7a1302577d5577aa922d7894f7481e2e0b7f
- `debian-binary` - d526eb4e878a23ef26ae190031b4efd2d58ed66789ac049ea3dbaf74c9df7402

## Key-file hashes - OBSERVED

- `extracted/package/var/jb/Library/MobileSubstrate/DynamicLibraries/VCamRecovered.dylib` - `3c325b3749733cdc6664577760d451c03b67b235f0118285ad8ec251c6f61fdc`
- `extracted/package/var/jb/Library/MobileSubstrate/DynamicLibraries/VCamRecovered.plist` - `07e2d4397b5f4f87a85f2c12445ce97c4c1c7bb17060a363e4c19788bffa2319`
- `extracted/package/var/jb/var/mobile/Library/Preferences/com.if-she.cydia.vcam.plist` - `c9265703e5aae0df5008307f2536f86038dd81a0da1e45cd83b91f7253d06a47`

The corresponding files under `recovered/` are byte-identical convenience copies; validation compares SHA-256 values before publication.

## Mach-O - OBSERVED

`VCamRecovered.dylib` is a thin **Mach-O 64-bit arm64 dynamically linked shared library**. The Mach-O `LC_BUILD_VERSION` records:

- platform: iOS
- minimum OS: **14.0**
- SDK: **16.4**
- linker tool version: 15.0.2

The full load-command evidence is preserved in `analysis/macho/VCamRecovered.otool-l.txt`. Apple `lipo` and `otool` were not installed in this Linux analysis environment; `file(1)` and LLVM 17 `llvm-objdump --macho` were used as read-only equivalents. No Mach-O bytes were modified.

## Dynamic dependencies - OBSERVED

```text
/mnt/data/IOS-15-USB-bootstrap-stage/recovered/VCamRecovered.dylib:
	@rpath/VCamRecovered.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libobjc.A.dylib (compatibility version 1.0.0, current version 228.0.0)
	/System/Library/Frameworks/Foundation.framework/Foundation (compatibility version 300.0.0, current version 1971.0.0)
	/System/Library/Frameworks/CoreFoundation.framework/CoreFoundation (compatibility version 150.0.0, current version 1971.0.0)
	/System/Library/Frameworks/UIKit.framework/UIKit (compatibility version 1.0.0, current version 6441.1.101)
	/System/Library/Frameworks/AVFoundation.framework/AVFoundation (compatibility version 1.0.0, current version 2.0.0)
	/System/Library/Frameworks/CoreMedia.framework/CoreMedia (compatibility version 1.0.0, current version 1.0.0)
	/System/Library/Frameworks/CoreVideo.framework/CoreVideo (compatibility version 1.2.0, current version 1.5.0)
	/System/Library/Frameworks/MobileCoreServices.framework/MobileCoreServices (compatibility version 1.0.0, current version 1228.0.0)
	/System/Library/Frameworks/CoreGraphics.framework/CoreGraphics (compatibility version 64.0.0, current version 1690.5.4)
	/System/Library/Frameworks/VideoToolbox.framework/VideoToolbox (compatibility version 1.0.0, current version 1.0.0)
	/System/Library/Frameworks/Security.framework/Security (compatibility version 1.0.0, current version 60420.102.1)
	/System/Library/Frameworks/CoreLocation.framework/CoreLocation (compatibility version 1.0.0, current version 2785.1.32)
	@rpath/CydiaSubstrate.framework/CydiaSubstrate (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libMobileGestalt.dylib (compatibility version 1.0.0, current version 1.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 1500.65.0)
	/System/Library/Frameworks/CoreImage.framework/CoreImage (compatibility version 1.0.0, current version 5.0.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1319.100.3)
```

## Injection plist - OBSERVED

```text
{
  "Filter" => {
    "Bundles" => [
      0 => "com.apple.mediaserverd"
      1 => "com.apple.springboard"
      2 => "com.apple.UIKit"
    ]
    "Executables" => [
      0 => "mediaserverd"
    ]
  }
}
```

The plist explicitly names `mediaserverd` in its filter data. This is an observed configuration fact; it is not proof that injection succeeds on iOS 15.8.8.

## Preference plist - OBSERVED

The preserved historical preference plist contains authentication/login-state related configuration fields. Literal credential-like field values are intentionally not duplicated in this public audit narrative. The original plist bytes remain preserved unchanged in the extracted package and recovered archival copy.
## Strings - OBSERVED

A complete unfiltered strings dump is preserved at `analysis/strings/VCamRecovered.strings.txt`. Selected strings containing terms relevant to the historical audit include:

```text
%VCamRecovered.dylib.3d6dcdfa.unsigned
/System/Library/Frameworks/CoreMedia.framework/CoreMedia
/System/Library/Frameworks/CoreVideo.framework/CoreVideo
/System/Library/Frameworks/VideoToolbox.framework/VideoToolbox
/var/jb/var/mobile/Library/Preferences/com.if-she.cydia.vcam.plist
@_CMSampleBufferCreateReady
@_CMSampleBufferGetImageBuffer
@_CVPixelBufferGetHeight
@_CVPixelBufferGetPixelFormatType
@_CVPixelBufferGetWidth
@_CVPixelBufferLockBaseAddress
@_CVPixelBufferRelease
@_CVPixelBufferRetain
@_CVPixelBufferUnlockBaseAddress
@_kCVPixelBufferOpenGLESCompatibilityKey
@_kCVPixelBufferPixelFormatTypeKey
@rpath/VCamRecovered.dylib
GET /vcam.mjpg HTTP/1.1
VCam
VCam Login
VCamButton
VCamManager
VCamOverlayWindow
VCamRecovered.dylib.3d6dcdfa.unsigned
[VCam] Heartbeat error: %@
[VCam] Hooking CMSampleBufferGetImageBuffer
[VCam] VCam: Received termination signal, cleaning up...
_CMSampleBufferCreateReady
_CMSampleBufferGetImageBuffer
_CVPixelBufferGetHeight
_CVPixelBufferGetPixelFormatType
_CVPixelBufferGetWidth
_CVPixelBufferLockBaseAddress
_CVPixelBufferRelease
_CVPixelBufferRetain
_CVPixelBufferUnlockBaseAddress
_kCVPixelBufferOpenGLESCompatibilityKey
_kCVPixelBufferPixelFormatTypeKey
[authentication-related preference key omitted from public narrative]
com.apple.mediaserverd
com.vcam.mediaProcess
com.vcam.updateSettings
imageWithCVPixelBuffer:
mediaserverd
render:toCVPixelBuffer:
vcam_patched
```

Strings are evidence of embedded text only. A suggestive string does **not** by itself prove runtime behavior.

## Symbols - OBSERVED

The full symbol table and the subset of undefined symbols are preserved under `analysis/symbols/`. Undefined imports include Objective-C runtime and framework/library symbols represented in the Mach-O import metadata. These observations identify dependencies and callable references; they do not prove which execution paths run on a particular device/runtime.

## Disassembly - OBSERVED / LIMITATION

A complete textual ARM64 disassembly generated by LLVM 17 is preserved at `analysis/disassembly/VCamRecovered.disassembly.txt`. It provides static machine-code evidence and supports later review of control flow and imported calls.

**No source code was recovered merely because disassembly exists.** The disassembly is not original source and no decompiled pseudocode is represented as original source.

## Historical behavior - evidence classification

**OBSERVED:**

- rootless package paths under `/var/jb`;
- MobileSubstrate dependency in package metadata;
- injection-filter configuration naming `mediaserverd`;
- arm64 Mach-O dylib with minimum iOS 14.0 and SDK 16.4;
- CoreMedia/CoreVideo/VideoToolbox and other dynamic dependencies/import evidence preserved in the static outputs;
- preference data included in the original package.

**INFERRED / NOT PROVEN:**

- static imports, strings, symbols, and disassembly can suggest intended historical mechanisms, but do not independently prove successful injection, frame replacement, USB operation, or compatibility with any particular iOS runtime.

**NOT PROVEN:**

- iOS 15.8.8 runtime compatibility;
- operation on the current target iPhone 6s Plus;
- Dopamine/ElleKit runtime behavior;
- current VCAM PRO architecture or implementation;
- applicability of IOS-16 techniques to this package.

## Immutability and limitations

- Original `.deb` preserved byte-for-byte.
- Raw `ar` members preserved byte-for-byte using their actual member names.
- Extracted dylib/plists were not patched, stripped, signed, relinked, converted in place, recompressed, or rebuilt.
- No `strip`, `codesign`, `ldid`, `install_name_tool`, binary patching, load-command modification, or plist replacement was performed.
- No device validation was performed.
- No package was installed or executed.
- No claim is made that IOS-16 techniques apply to this historical package.
- Repository purpose: **HISTORICAL REFERENCE ONLY**.


## Public archive publication note

This `AUDIT.md` is a public-safe derivative of the historical audit document.

Historical pre-publication `AUDIT.md` SHA-256:

`1b1dbc6a1c126a2e6657f6214f5e6ef818e165e381022e5388a4d99ce694ceb1`

Sanitization affects only duplicated narrative text in this audit document. The original `.deb`, package contents, binary, plist, and disassembly bytes are unchanged. The raw historical preference artifact remains part of the archived package. No functional behavior was modified, and no credential from VCAM-PRO, GitHub, or VPS was inserted into this public audit narrative.

## Governance

`martaxi-boss/IOS-15-USB`  
**STATUS AFTER BOOTSTRAP: READ ONLY**

**NO FURTHER DEVELOPMENT AUTHORIZED.**

**ALL NEW VCAM PRO DEVELOPMENT:**  
`martaxi-boss/VCAM-PRO`
