# 🤖 Android Custom ROM & Firmware Notes

A technical log covering aftermarket Android firmware installation, recovery management, partition structures, and my ongoing journey toward compiling custom ROMs from source.

---

## 📋 Pre-Flash Safety Checklist
- [x] Verify exact model number and hardware architecture (`arm64-v8a`)
- [x] Back up critical device-specific partitions (`EFS` / `sec_efs` for IMEI, `persist`)
- [x] Unlock OEM Bootloader (`Download Mode` / `Odin` / `Fastboot`)
- [x] Verify firmware/modem baseline matches the target Custom ROM requirements

---

## ⚡ Core ADB, Fastboot & Recovery Workflow

### 1. Device Connection & Reboot Modes
* `adb devices` — Verify USB debugging connection and authorization
* `adb reboot bootloader` — Reboot into Fastboot mode
* `adb reboot download` — Reboot into Download/Odin mode (Samsung devices)
* `adb reboot recovery` — Reboot directly into custom recovery (`TWRP` / `LineageOS Recovery`)

### 2. Flashing & Sideloading
* `fastboot flash recovery <recovery.img>` — Flash custom recovery image to the recovery partition
* `fastboot flash boot <boot.img>` — Flash kernel/boot image
* `adb sideload <rom-build.zip>` — Sideload custom ROM zip via Recovery
* `adb sideload <MindTheGapps-arm64.zip>` — Sideload Google Mobile Services (ARM64) before first boot to preserve permissions and passkey support

---

## 🗂️ Key Android Partition Reference
| Partition | Function |
| :--- | :--- |
| `/boot` | Linux kernel and ramdisk |
| `/system` | Core Android OS framework and system applications |
| `/vendor` | SoC-specific proprietary blobs and hardware abstraction layers (HALs) |
| `/product` & `/odm` | Device-specific customizations and hardware configurations |
| `/data` | User data, installed apps, and internal storage |
| `/efs` | Encrypted hardware identifiers (IMEI, MAC address, radio calibration) |

---

## 🛠️ Future Roadmap (ROM Compilation)
- [ ] Set up a Linux build environment for AOSP / LineageOS compilation
- [ ] Learn Device Tree (`device/<vendor>/<codename>`), Vendor Blobs, and Kernel source integration
- [ ] Explore One UI port frameworks (e.g., debloating and modifying system packages)
