# SDK Platform-Tools for Windows

A complete Windows toolkit for working with Android devices through **ADB (Android Debug Bridge)** and **Fastboot**.

Platform-Tools are commonly used for Android development, debugging, device management, recovery/bootloader operations, firmware flashing, and troubleshooting.

> **Important:** Always use the official Android SDK Platform-Tools package from Google. Do not download modified or unknown copies.

---

## 📋 Table of Contents

- [Features](#-features)
- [Included Tools](#-included-tools)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [USB Driver Setup](#-usb-driver-setup)
- [Enable USB Debugging](#-enable-usb-debugging)
- [Verify ADB](#-verify-adb)
- [ADB Commands](#-adb-commands)
- [APK Management](#-apk-management)
- [File Transfer](#-file-transfer)
- [Device Information](#-device-information)
- [Logs and Debugging](#-logs-and-debugging)
- [ADB Shell](#-adb-shell)
- [Reboot Commands](#-reboot-commands)
- [Fastboot Commands](#-fastboot-commands)
- [Bootloader Operations](#-bootloader-operations)
- [Recovery Operations](#-recovery-operations)
- [Wireless ADB](#-wireless-adb)
- [Multiple Devices](#-multiple-devices)
- [Windows PATH Setup](#-windows-path-setup)
- [Troubleshooting](#-troubleshooting)
- [Safety](#-safety)
- [Useful Workflows](#-useful-workflows)
- [FAQ](#-faq)
- [Official Resources](#-official-resources)

---

# 🚀 Features

- Android Debug Bridge (ADB)
- Fastboot device management
- APK installation and removal
- Application debugging
- File transfer
- Android shell access
- Log collection with Logcat
- Device information
- Screen capture
- Device reboot control
- Bootloader access
- Recovery access
- Wireless ADB
- Multiple-device management
- Windows command-line support
- Android development support

---

# 🧰 Included Tools

The Platform-Tools package primarily provides:

| Tool | Purpose |
|---|---|
| `adb.exe` | Android Debug Bridge |
| `fastboot.exe` | Bootloader/Fastboot communication |
| `AdbWinApi.dll` | ADB Windows API |
| `AdbWinUsbApi.dll` | ADB USB communication |

Additional files may be included depending on the Platform-Tools release.

---

# 💻 Requirements

### Operating System

- Windows 10
- Windows 11
- 64-bit Windows recommended

### Hardware

- Windows PC
- USB cable
- Android device

### Optional

- Android USB drivers
- Android Studio
- PowerShell
- Command Prompt

---

# 📥 Installation

## 1. Download Platform-Tools

Download the latest **official SDK Platform-Tools for Windows** package from Google.

Extract the ZIP file to a location such as:

```text
C:\platform-tools
```

The folder should contain:

```text
C:\platform-tools\
├── adb.exe
├── fastboot.exe
├── AdbWinApi.dll
├── AdbWinUsbApi.dll
└── ...
```

---

# 🔌 USB Driver Setup

Windows may require a USB driver before ADB or Fastboot can communicate correctly with your Android device.

Depending on the manufacturer, you may need:

- Google USB Driver
- Samsung USB Driver
- Xiaomi USB Driver
- Motorola USB Driver
- OnePlus USB Driver
- Other manufacturer-specific drivers

After installing the appropriate driver:

1. Connect the Android device.
2. Open **Device Manager**.
3. Check **Android Devices**, **Portable Devices**, or **Other Devices**.
4. Confirm that Windows recognizes the device.

---

# ⚙️ Enable USB Debugging

On the Android device:

1. Open **Settings**.
2. Open **About Phone**.
3. Find **Build Number**.
4. Tap **Build Number** approximately seven times.
5. Developer Options will become available.
6. Open **Developer Options**.
7. Enable **USB Debugging**.

The exact menu location can vary between Android manufacturers.

---

# 🔍 Verify ADB

Open PowerShell or Command Prompt inside the Platform-Tools folder.

Run:

```powershell
adb version
```

Example:

```text
Android Debug Bridge version ...
```

Then connect your Android device and run:

```powershell
adb devices
```

Example:

```text
List of devices attached
XXXXXXXX    device
```

If the phone displays an RSA authorization prompt, unlock the phone and select:

**Allow USB debugging**

---

# 📱 ADB Commands

## List Devices

```powershell
adb devices
```

Detailed device information:

```powershell
adb devices -l
```

---

## Restart ADB

```powershell
adb kill-server
adb start-server
```

Then:

```powershell
adb devices
```

---

# 📦 APK Management

## Install APK

```powershell
adb install app.apk
```

Install with replacement:

```powershell
adb install -r app.apk
```

Install multiple APK files:

```powershell
adb install-multiple base.apk split_config.apk
```

Uninstall an application:

```powershell
adb uninstall com.example.app
```

---

# 📂 File Transfer

## PC → Android

```powershell
adb push file.txt /sdcard/
```

Example:

```powershell
adb push app.apk /sdcard/Download/
```

## Android → PC

```powershell
adb pull /sdcard/file.txt .
```

Example:

```powershell
adb pull /sdcard/Download/app.apk .
```

---

# 📋 Device Information

Android version:

```powershell
adb shell getprop ro.build.version.release
```

Android SDK version:

```powershell
adb shell getprop ro.build.version.sdk
```

Device model:

```powershell
adb shell getprop ro.product.model
```

Manufacturer:

```powershell
adb shell getprop ro.product.manufacturer
```

Serial number:

```powershell
adb get-serialno
```

All system properties:

```powershell
adb shell getprop
```

---

# 🐛 Logs and Debugging

View Android logs:

```powershell
adb logcat
```

Save logs to a file:

```powershell
adb logcat > log.txt
```

Clear existing logs:

```powershell
adb logcat -c
```

Display only errors:

```powershell
adb logcat *:E
```

Stop Logcat:

```text
CTRL + C
```

---

# 🖥️ ADB Shell

Open an Android shell:

```powershell
adb shell
```

Run a single command:

```powershell
adb shell ls
```

Check storage:

```powershell
adb shell df -h
```

Check running processes:

```powershell
adb shell ps
```

Exit the shell:

```bash
exit
```

---

# 🔄 Reboot Commands

Normal reboot:

```powershell
adb reboot
```

Recovery:

```powershell
adb reboot recovery
```

Bootloader:

```powershell
adb reboot bootloader
```

Fastboot:

```powershell
adb reboot fastboot
```

> Not every device supports every reboot mode.

---

# ⚡ Fastboot

Fastboot communicates with Android devices while they are in the bootloader/fastboot environment.

Check connected Fastboot devices:

```powershell
fastboot devices
```

Display Fastboot variables:

```powershell
fastboot getvar all
```

> Some devices intentionally hide or restrict certain variables.

---

# 🔓 Bootloader Operations

Reboot to bootloader:

```powershell
adb reboot bootloader
```

Then check:

```powershell
fastboot devices
```

Unlocking a bootloader is **device-specific**.

Do not run random unlock commands without checking your manufacturer's official documentation.

Bootloader unlocking can:

- Erase user data
- Disable certain security features
- Affect warranty/support
- Prevent normal boot if incorrect procedures are used

---

# 💾 Flashing

Fastboot can be used for firmware and partition operations on devices that support them.

Typical examples include:

```powershell
fastboot flash boot boot.img
```

or:

```powershell
fastboot flash recovery recovery.img
```

However, **partition names and supported flashing commands vary by device**.

Never assume that a command for one Android phone will work on another.

---

# 🔄 Recovery Operations

To enter recovery:

```powershell
adb reboot recovery
```

Alternatively:

```powershell
adb reboot bootloader
```

and select the appropriate recovery option on supported devices.

Recovery software such as stock recovery, TWRP, or other custom recoveries may provide different features.

---

# 📡 Wireless ADB

Modern Android versions can support wireless debugging.

On supported devices:

1. Enable Developer Options.
2. Enable **Wireless Debugging**.
3. Pair the PC with the device.
4. Use the pairing command displayed by Android.

Example:

```powershell
adb pair IP_ADDRESS:PAIRING_PORT
```

Then connect:

```powershell
adb connect IP_ADDRESS:PORT
```

Check:

```powershell
adb devices
```

Wireless debugging requires the PC and Android device to have suitable network connectivity.

---

# 🔢 Multiple Devices

If multiple Android devices are connected:

```powershell
adb devices
```

Specify a device:

```powershell
adb -s DEVICE_SERIAL shell
```

Install an APK on a specific device:

```powershell
adb -s DEVICE_SERIAL install app.apk
```

---

# 🛣️ Add Platform-Tools to Windows PATH

Adding Platform-Tools to PATH allows you to run:

```powershell
adb
```

and:

```powershell
fastboot
```

from any Command Prompt or PowerShell window.

## Steps

1. Open Windows Search.
2. Search for:

```text
Environment Variables
```

3. Open **Edit the system environment variables**.
4. Select **Environment Variables**.
5. Under User Variables, select `Path`.
6. Click **Edit**.
7. Click **New**.
8. Add:

```text
C:\platform-tools
```

9. Save all dialogs.
10. Open a new terminal.

Test:

```powershell
adb version
```

and:

```powershell
fastboot --version
```

---

# 🧪 Useful ADB Workflow

### Check connection

```powershell
adb devices
```

### Get device information

```powershell
adb shell getprop ro.product.model
```

### Install application

```powershell
adb install app.apk
```

### Open shell

```powershell
adb shell
```

### Collect logs

```powershell
adb logcat > device-log.txt
```

### Reboot

```powershell
adb reboot
```

---

# 🛠️ Troubleshooting

## `adb is not recognized`

Possible causes:

- Platform-Tools is not in PATH.
- Terminal was opened before PATH was updated.
- Incorrect Platform-Tools directory.

Try:

```powershell
cd C:\platform-tools
.\adb.exe version
```

---

## Device shows `unauthorized`

Unlock the Android device and accept:

**Allow USB debugging**

If necessary:

```powershell
adb kill-server
adb start-server
adb devices
```

---

## Device does not appear

Check:

- USB cable
- USB port
- USB drivers
- USB debugging
- Android device notification/USB mode
- Windows Device Manager

Try:

```powershell
adb kill-server
adb start-server
adb devices
```

---

## Fastboot device does not appear

Check:

```powershell
fastboot devices
```

If nothing appears:

- Verify the device is actually in Fastboot mode.
- Check USB drivers.
- Try another USB port.
- Try another cable.
- Check Device Manager.

---

## `waiting for device`

This usually indicates a communication or driver problem.

Check:

```powershell
adb devices
```

or:

```powershell
fastboot devices
```

depending on the mode.

---

# 🔐 Security

ADB provides powerful access to an Android device.

Never authorize USB debugging on an untrusted computer.

Avoid:

- Unknown ADB commands
- Unknown scripts
- Modified Platform-Tools packages
- Random firmware files
- Unverified boot images
- Commands copied from unreliable sources

---

# ⚠️ Safety

Fastboot commands can modify critical Android partitions.

Before flashing anything:

1. Confirm the exact device model.
2. Confirm the exact device variant.
3. Confirm the correct firmware/image.
4. Read the manufacturer's documentation.
5. Back up important data.
6. Understand whether the operation will erase data.

**Never flash an image simply because its filename looks compatible.**

---

# 🧰 Developer Usage

Platform-Tools are useful for:

- Android application development
- Flutter development
- React Native development
- Android Studio workflows
- Device debugging
- QA testing
- Automated testing
- APK deployment
- Android recovery troubleshooting
- Bootloader operations
- Firmware maintenance

For Flutter development, verify the Android device with:

```powershell
adb devices
```

Then:

```powershell
flutter devices
```

---

# 📁 Recommended Folder Structure

```text
C:\
└── platform-tools\
    ├── adb.exe
    ├── fastboot.exe
    ├── AdbWinApi.dll
    ├── AdbWinUsbApi.dll
    └── ...
```

Keep Platform-Tools in a simple directory without unnecessary modifications.

---

# 📜 License & Distribution

Android SDK Platform-Tools are provided by Google and are subject to Google's applicable license terms.

If this repository redistributes Platform-Tools binaries, ensure that the redistribution complies with the current official Google licensing and distribution requirements.

This README does **not** grant permission to redistribute Google's binaries.

---

# 🏢 Credits

**Android SDK Platform-Tools**

Developed and maintained by **Google / Android Developers**.

This project is not affiliated with or endorsed by Google unless explicitly stated.

---

# 🔗 Official Resources

- Android Developers
- Android SDK Platform-Tools
- Android Debug Bridge (ADB)
- Fastboot documentation
- Android Developer documentation

---

# 📌 Quick Reference

| Task | Command |
|---|---|
| Check ADB | `adb version` |
| List devices | `adb devices` |
| Detailed devices | `adb devices -l` |
| Restart ADB | `adb kill-server && adb start-server` |
| Install APK | `adb install app.apk` |
| Uninstall APK | `adb uninstall package.name` |
| Push file | `adb push file /sdcard/` |
| Pull file | `adb pull /sdcard/file .` |
| Shell | `adb shell` |
| Logs | `adb logcat` |
| Reboot | `adb reboot` |
| Recovery | `adb reboot recovery` |
| Bootloader | `adb reboot bootloader` |
| Fastboot devices | `fastboot devices` |
| Fastboot version | `fastboot --version` |

---

## ⭐ Support

If you find this project useful, consider giving it a ⭐ on GitHub.

**Use Android Platform-Tools responsibly and always verify commands before executing them.**
