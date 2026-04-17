# 🔥 FireStorm Challenge - Reverse Engineering with Frida

**Course:** Mobile Application Security  
**Analyst:** Omar Haouani  
**Target APK:** FireStorm.apk  
**Date:** April 2026

---

## 📋 Table of Contents

1. [Introduction](#introduction)
2. [Technical Environment](#technical-environment)
3. [Phase 1: Environment Setup](#phase-1-environment-setup)
4. [Phase 2: Static Analysis with JADX](#phase-2-static-analysis-with-jadx)
5. [Phase 3: Frida Instrumentation](#phase-3-frida-instrumentation)
6. [Phase 4: Firebase Authentication](#phase-4-firebase-authentication)
7. [Final Flag](#final-flag)
8. [Execution Flow](#execution-flow)
9. [Security Recommendations](#security-recommendations)
10. [Checklist](#checklist)

---

## Introduction

This lab focuses on **advanced reverse engineering** of an Android application using a native library to dynamically generate a password. The goal is to extract this password using **Frida**, then authenticate to **Firebase** to retrieve the final flag.

### Challenge Objectives

| # | Objective |
|---|-----------|
| 1 | Statically analyze the APK with JADX-GUI |
| 2 | Understand the password generation mechanism |
| 3 | Instrument the app with Frida to capture the password |
| 4 | Extract Firebase configuration from `strings.xml` |
| 5 | Develop a Python script for authentication |
| 6 | Retrieve and validate the final flag |

---

## Technical Environment

| Tool | Version |
|------|---------|
| JADX-GUI | Latest |
| Frida | 17.9.1 |
| Python | 3.14.3 |
| Pyrebase | Latest |
| ADB | 1.0.41 |
| Emulator | Android Emulator 5554 |

---

## Phase 1: Environment Setup

### APK Installation

![APK Installation](1.png)

### Frida Process Verification

![Frida Processes](1.png)

**Result:** FireStorm detected (PID 8424)

| Application | PID |
|-------------|-----|
| Firestorm | 8424 |
| Chrome | 9342 |
| Google Play Services | 7850 |
| Phone | 6078 |

### Starting Frida Server

![Frida Server Setup](2.png)

---

## Phase 2: Static Analysis with JADX

### Application Structure

| Component | Value |
|-----------|-------|
| Package | `com.pwnsec.firestorm` |
| Main Activity | `MainActivity` |
| Native Library | `libfirestorm.so` |

### Password() Method Analysis

![JADX Password Method](3.png)

### Firebase Configuration from strings.xml

![Firebase Strings](4.png)

| Key | Value |
|-----|-------|
| `firebase_database_url` | https://firestorm-9d3db-default-rtdb.firebaseio.com |
| `firebase_email` | TK757567@pwsec.xyz |
| `google_api_key` | AIzaSyAXsK0qxs4RuLSA9C8IPSWd0eQ67HVHuJY |

---

## Phase 3: Frida Instrumentation

### JavaScript Script (frida_firestorm.js)

![Frida Script](CODEJS.png)

### Executing Frida Script

![Frida Execution](5.png)

**Capture Result:**

| Element | Value |
|---------|-------|
| Instance found | `com.pwnsec.firestorm.MainActivity@8cfd49a` |
| Password generated | `C7_dotpsC7t7f_._In_i.IdtpaofoaIDIdnndIfC` |

---

## Phase 4: Firebase Authentication

### Python Script (get_flag.py)

![Python Script](CODEPY.png)

### Flag Retrieval

![Flag Retrieved](6.png)

---

## Final Flag
PWNSEC{C0ngr4ts_Th4t_w45_4N_345y_P4$$w0rd_t0_G3t!!!!0R!5_!t????}

text

---

## Execution Flow
FireStorm.apk
↓
JADX - Static Analysis
↓
Password() → String concatenation from strings.xml
↓
generateRandomString() → Native method (libfirestorm.so)
↓
Frida - Hooking
↓
Password capture
↓
Python Script - Pyrebase
↓
Firebase Authentication
↓
Flag Retrieved

text

---

## Summary of Findings

| Component | Extraction Method | Value Found |
|-----------|------------------|-------------|
| Firebase Email | strings.xml | TK757567@pwsec.xyz |
| Firebase API Key | strings.xml | AIzaSyAXsK0qxs4RuLSA9C8IPSWd0eQ67HVHuJY |
| Database URL | strings.xml | https://firestorm-9d3db-default-rtdb.firebaseio.com |
| Password | Frida Hooking | C7_dotpsC7t7f_._In_i.IdtpaofoaIDIdnndIfC |
| Flag | Firebase Auth | PWNSEC{C0ngr4ts_...} |

---

## Security Recommendations

- Never hardcode API keys or Firebase URLs in `strings.xml`
- Protect native libraries with obfuscation (Obfuscator-LLVM)
- Implement certificate pinning to prevent interception
- Add anti-hooking mechanisms (Frida detection, ptrace, etc.)
- Use Firebase App Check to validate request origins
- Secure storage of secrets in Android Keystore

---

## Checklist

- [x] FireStorm.apk installed on emulator
- [x] Frida Server verified and running
- [x] Static analysis with JADX - Password() method
- [x] Firebase configuration extracted from strings.xml
- [x] Frida script developed
- [x] Frida execution - password captured
- [x] Python Pyrebase script developed
- [x] Firebase authentication successful
- [x] Flag retrieved and validated

---

## Resources

- [Frida Documentation](https://frida.re/docs/)
- [Pyrebase for Python](https://github.com/n皮/pyrebase)
- [ADB Documentation](https://developer.android.com/studio/command-line/adb)

---

*© 2026 - Mobile Application Security Course - Omar Haouani*
