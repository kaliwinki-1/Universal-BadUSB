# Universal BadUSB: The Base64-Only Framework
### The Zero-Fail Standard for HID Injection / Le Standard Zéro-Échec pour l'Injection HID

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![PowerShell](https://img.shields.io/badge/PowerShell-5.0%2B-blue?style=flat&logo=powershell)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=flat&logo=windows)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 🇺🇸 English Version

### Project Overview
The single greatest point of failure in BadUSB (Human Interface Device) attacks is **Keyboard Layout Incompatibility**.
A payload designed for a US (QWERTY) keyboard will catastrophically fail on a French (AZERTY), German (QWERTZ), or Spanish system. Critical symbols like `\`, `/`, `:`, `_`, and `$` are located on different physical keys across the world.

This repository provides a **Hardware-Agnostic Framework** (Flipper Zero, Rubber Ducky, DigiSpark, ESP32) to guarantee **100% execution reliability** on any Windows target, regardless of its language or keyboard configuration.

### The Philosophy: The "Common Denominator"
Instead of trying to guess the target's layout, we bypass the layout entirely. We utilize **Systematic Base64 Encoding**.

While letters like Q, A, Z, and W may shift between regions, the Base64 encoding method removes the dependency on the complex symbols that cause 90% of injection failures. By encoding payloads into Base64 and injecting them via PowerShell's native decoder, we achieve near-universal compatibility once the environment is normalized.

### Phase 1: The Environment Normalizer
Before running any complex payload, you must **normalize the target environment**.
This script forces Windows to recognize the **US-International layout** using a Base64-encoded command. This "cleans" the environment for any future scripts, ensuring that all subsequent keystrokes are interpreted correctly.

**File:** `01_Environment_Normalizer.txt`
```plaintext
REM --- UNIVERSAL LANGUAGE NORMALIZER ---
REM Description: Forces Windows to load the en-US keyboard layout.
REM Compatibility: Universal (AZERTY/QWERTY/QWERTZ)
REM Method: PowerShell -EncodedCommand (Base64)

DELAY 3000
GUI r
DELAY 500
STRING powershell -e JABsAD0ATgBlAHcALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgAGUAbgAtAFUAUwA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQwBsAGUAYQByACgAKQA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQQBkAGQAKAAnADAANAAwADkAOgAwADAAMAAyADAANAAwADkAJwApADsAUwBlAHQALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgACQAbAAgAC0ARgBvAHIAYwBlAA==
ENTER
