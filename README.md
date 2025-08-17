## Canaima CNM8183 / QT2308BK — Firmware Preservation & Dump Guide

![Project](https://img.shields.io/badge/Project-Firmware_Preservation-5A67D8?style=for-the-badge&logo=github&logoColor=white&labelColor=101010)
![Device](https://img.shields.io/badge/Device-CNM8183_/_QT2308BK-0EA5E9?style=for-the-badge&logo=android&logoColor=white&labelColor=101010)
![Firmware](https://img.shields.io/badge/Firmware-cnm8183__v1.0__20240629-22C55E?style=for-the-badge&logo=buffer&logoColor=white&labelColor=101010)
![Chipset](https://img.shields.io/badge/Platform-MediaTek_MT8183_-F59E0B?style=for-the-badge&logo=mediatek&logoColor=white&labelColor=101010)
![License](https://img.shields.io/badge/Docs_License-CC_BY_4.0-4B5563?style=for-the-badge&logo=creativecommons&logoColor=white&labelColor=101010)

> **Goal**: Preserve the **original firmware** of the **Canaima CNM8183 / QT2308BK Tablet** and provide a clear, reproducible guide on how to **dump (extract)** the firmware using [**MTKClient**](https://github.com/bkerler/mtkclient).

---

## Firmware
### Firmware extracted cnm8183_v1.0_20240629 with android 13 in .img format files
You can download this firmware [here](https://pixeldrain.com/u/G3nkbvzW)

---

## Device Information

- **Model**: Tablet **Canaima CNM8183 / QT2308BK**  
- **Identified Firmware**: `cnm8183_v1.0_20240629`  
- **Architecture/SoC**: **MediaTek MT8183 platform**  
- **Motivation**: Preserve the **stock state**, create a verifiable backup, and document a **reproducible process**  

> **Tip**: You can verify the chipset and partition map with `mtk printgpt` and by recording the VID/PID when connecting in BROM mode. Instructions are included below.

---

## Installation & Usage

### Supported Systems

- **Linux**: Tested on Arch Linux  
- **Windows**: 10 / 11 (tested on Windows 11)  
- **macOS**: 12+  

### Required Software & Dependencies

- **Python** 3.9+  
- **Git**  
- **libusb/fuse** (Linux)  
- **Drivers** (Windows: MTK Port + UsbDk)  

### Installing MTKClient

> Refer to the official [MTK Client repository](https://github.com/bkerler/mtkclient) for installation and usage instructions (CLI/GUI) — project by **bkerler**.

---

## Usage

### Using MTKClient with GUI

1. Launch the graphical interface with:
```
python mtk_gui.py
```

2. Power off the tablet and connect it via USB to your PC (**IMPORTANT**: disconnect any keyboard) while holding both **volume up** and **volume down** buttons simultaneously.

3. In the tool, go to the "**Read partition(s)**" tab → check "**Select all partitions**" → click "**Read partition(s)**" and choose a folder to save the binaries.  

4. Wait for the process to finish and enjoy your freshly extracted firmware. ✅

---

### Rooting the Tablet

1. First, extract **boot.img** with the following command (or via the GUI):
```
python mtk.py r boot boot.img 
```
**GUI alternative:**
```
python mtk_gui.py 
```


2. Reboot the device:
```
python mtk.py reset
```

3. Download patched magisk for mtk:
Download latest Magisk [here](https://github.com/topjohnwu/Magisk/releases/latest)

4. Install on target phone
- you need to enable usb-debugging via Settings/About phone/Version, Tap 7x on build number
- Go to Settings/Additional settings/Developer options, enable "OEM unlock" and "USB Debugging"
- Install magisk apk
```
adb install app-release.apk
```
- accept auth rsa request on mobile screen of course to allow adb connection

5. Upload boot to /sdcard/Download
```
adb push boot.img /sdcard/Download
```

6. Start magisk, tap on Install, select boot.img from /sdcard/Download, then:
```
adb pull /sdcard/Download/[displayed magisk patched boot filename here]
mv [displayed magisk patched boot filename here] boot.patched
```

7. Do the steps needed in section "Unlock bootloader below"

8. Flash magisk-patched boot
```
python mtk.py w boot boot.patched
```

9. Reboot the phone
```
python mtk.py reset
```

10. Disconnect the USB cable and enjoy your rooted tablet. 🎉  

---

## Legal & Disclaimer

- This project is **for educational purposes** and aims to preserve the original firmware of your **own device**.  
- No proprietary images from the manufacturer are included in this repository (only guides, scripts, and verification hashes).  
- Do not share or redistribute dumps containing unique identifiers or manufacturer intellectual property without permission.  
- You are solely responsible for any modifications to your device. The author and contributors are **not liable** for damages, data loss, or device bricking.  

---

## Credits & References

- [MTKClient](https://github.com/bkerler/mtkclient) — Primary tool for MediaTek device read/write operations.  

Additional learning resources and backup/dump guides for MTK platforms.  

> If this guide helped you, consider giving the repo a ⭐, opening Issues with improvements, or submitting PRs with corrections ✨
