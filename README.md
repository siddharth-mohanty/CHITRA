# 📡 CHITRA

**C**onnected **H**otspot **I**nspection & **T**ethering **R**econnaissance **A**pp

A self-hosted, no-root diagnostic tool that inspects **your own** Android phone's WiFi and hotspot activity over USB — saved networks, current connection, hotspot clients, and recent connectivity logs — all pulled through ADB, no root required.

![Platform](https://img.shields.io/badge/platform-Linux-informational)
![License](https://img.shields.io/badge/license-MIT-green)
![No Root](https://img.shields.io/badge/root-not%20required-success)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![Distribution](https://img.shields.io/badge/source-closed-lightgrey)

```
==============================================================
|  ######   ##    ##  ########  ########  #######     ####   |
| ##    ##  ##    ##     ##        ##     ##    ##   ##  ##  |
| ##        ##    ##     ##        ##     ##    ##  ##    ## |
| ##        ##    ##     ##        ##     ##    ##  ##    ## |
| ##        ########     ##        ##     #######   ######## |
| ##        ##    ##     ##        ##     ##   ##   ##    ## |
| ##        ##    ##     ##        ##     ##    ##  ##    ## |
| ##    ##  ##    ##     ##        ##     ##    ##  ##    ## |
|  ######   ##    ##  ########     ##     ##    ##  ##    ## |
==============================================================
            Android WiFi / Hotspot Inspection Tool
                  (for your own device only)
```

---

## ⚠️ Before you use this

CHITRA is built to run **only against a device you personally own**, connected physically over USB with your own explicit consent. It does not, and cannot, access another person's phone remotely, break into anything, or bypass any security control — every piece of data it reads is exposed by Android's own official `adb` debugging interface, the same interface app developers use every day.

Please don't use this on a device that isn't yours, or on a network you don't have permission to inspect. 🙏

---

## ✨ What it actually does

| Feature | Description |
|---|---|
| 📱 **Device Info** | Manufacturer, model, Android version, serial number, Android ID |
| 📶 **Saved WiFi Networks** | Every network your phone has ever connected to (names only — **no passwords**, that's blocked by Android itself without root) |
| 🔐 **Password-Protected Networks** | A clean, de-duplicated list of just the secured networks |
| 📡 **Nearby BSSIDs** | Router MAC addresses for saved networks currently in range |
| 🌐 **Current Connection** | Live SSID, signal strength, link speed, IP address |
| 💻 **Other Devices on Your Network** | IP + MAC of other devices on your home WiFi (ARP-based) |
| 🔥 **Hotspot Status** | Whether your hotspot is on, and who's connected to it |
| 📜 **Recent WiFi Events** | Filtered, readable connectivity log — noise stripped out |
| 🔒 **Password Gate** | A simple local access gate so the tool doesn't run itself if someone else picks up your machine |

CHITRA **auto-downloads and manages its own copy of ADB** (Android Platform Tools) — you don't need to install anything separately.

---

## 🚫 What it will never show you

Because of Android's own security model (not a limitation of this tool):

- ❌ Saved WiFi **passwords** — blocked for all apps without root, full stop
- ❌ IMEI / hardware serial — blocked since Android 10, even for `adb shell`, without root
- ❌ Anyone else's device, remotely — everything requires a physical USB connection and your explicit "Allow USB debugging" tap on the phone itself

---

## 🚀 Getting started

Grab the latest Linux executable from the **[Releases](../../releases)** page.

```bash
chmod +x chitra
./chitra
```

> 📦 This project is distributed as a **precompiled Linux binary only** — source code is not published in this repository.

### On your phone (one-time setup)

1. Settings → About Phone → tap **Build Number** 7 times → unlocks Developer Options
2. Developer Options → enable **USB Debugging**
3. Plug your phone into your computer via USB
4. Tap **Allow** on the "Allow USB debugging?" popup that appears on your phone

### Default password

> ⚠️ **Restricted use notice:** This tool is intended strictly for law enforcement, authorized security personnel, or use with the explicit prior permission of the developer. Do not use this tool without proper authorization.

---

## 📸 Sample output

```
============================================================
DEVICE INFO
============================================================
Field               Value
------------------------------------------------------------
Manufacturer        <your phone's manufacturer>
Model               <your phone's model>
Android version     <version>
...

============================================================
HOTSPOT / TETHERING STATUS
============================================================
Hotspot status      ON - broadcasting as a hotspot
Devices connected   1

IP Address          MAC Address
------------------------------------------------------------
<device IP>         <device MAC>
```

---

## 🧩 How it works, briefly

CHITRA talks to your phone entirely through **ADB** (Android Debug Bridge) — the same official tool Google ships for app developers. Under the hood, it runs standard, publicly documented ADB commands such as `list-networks`, `dumpsys wifi`, and reads from the phone's own neighbor/ARP tables — nothing here touches a private API, exploits anything, or requires root. It reads exactly what Android already exposes to any authorized ADB session.

---

## 🤝 Contributing

This repository distributes a precompiled binary only, so code contributions aren't accepted directly here. If you run into a bug, please open an issue describing what happened (your Android version, OEM, and what output you saw) so it can be investigated.

---

## 📄 License

Released under the [MIT License](LICENSE) — free to use, modify, and share.

---

## ⚖️ Disclaimer

This tool is provided for personal device diagnostics and learning purposes only. The author is not responsible for any misuse. Always ensure you have explicit authorization before inspecting any device or network that isn't your own.

---

<p align="center">Made with 🖤 and a lot of <code>adb shell</code> commands</p>
