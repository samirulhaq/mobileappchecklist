
# Mobile Application Security Assessment Checklist
**Version:** 1.0
**Date:** January 08, 2026
**Target:** Android / iOS

---

## 1. Executive Summary
This document outlines the security assessment criteria for the target mobile application. It includes standard checks (OWASP MASVS) and a specialized section for "Out of the Box" logic vulnerabilities.

---

## 2. Static Analysis (SAST)
*Analysis of source code, configuration files, and binaries.*

- [ ] **SA-01: Manifest Debugging**
    * Verify `android:debuggable="false"` in release builds.
- [ ] **SA-02: Backup Configuration**
    * Verify `android:allowBackup="false"` to prevent ADB data extraction.
- [ ] **SA-03: Exported Components**
    * Ensure Activities/Services are not exported (`exported="true"`) without permissions.
- [ ] **SA-04: App Transport Security (iOS)**
    * Ensure `NSAllowsArbitraryLoads` is `false`.
- [ ] **SA-05: Hardcoded Secrets**
    * Scan code/strings for "API Key", "Bearer", "AWS", "Private Key".
- [ ] **SA-06: Code Obfuscation**
    * Verify ProGuard/R8 is applied to impede reverse engineering.
- [ ] **SA-07: Root/Jailbreak Detection**
    * Verify the app detects compromised environments.

---

## 3. Data Storage & Privacy
*Assessment of data at rest.*

- [ ] **DS-01: Insecure Storage**
    * Check SharedPrefs/NSUserDefaults for plain-text tokens/PII.
- [ ] **DS-02: Local Database Encryption**
    * Ensure SQLite/Realm DBs use encryption (e.g., SQLCipher).
- [ ] **DS-03: Log Leakage**
    * Verify no sensitive data is printed to Logcat/Console during usage.
- [ ] **DS-04: Clipboard Restriction**
    * Ensure sensitive fields (passwords/OTP) disable copy/paste.
- [ ] **DS-05: Background Snapshots**
    * Verify app screen is blurred/hidden in the OS task switcher.
- [ ] **DS-06: Cache Leakage**
    * Check `Cache/` directories for stored sensitive HTTP responses.

---

## 4. "Out of the Box" & Logic Vulnerabilities
*Creative attack vectors focusing on business logic.*

### Business Logic
- [ ] **OTB-01: The "Offline" Bypass**
    * Disable internet -> Attempt to access Premium features.
- [ ] **OTB-02: Race Conditions**
    * Attempt simultaneous coupon redemption or transfers from two devices.
- [ ] **OTB-03: Negative Quantity**
    * Intercept cart requests; set quantity to `-1`. Check for refunds/credits.

### Platform Abuse & Deep Links
- [ ] **OTB-04: Deep Link Hijacking**
    * Can malicious links (`app://token=...`) trigger account takeover?
- [ ] **OTB-05: Internal WebView XSS**
    * Do deep links reflect parameters inside internal WebViews?
- [ ] **OTB-06: Android Intent Injection**
    * Can malicious apps invoke exported activities to bypass auth steps?

### Authentication & Hardware
- [ ] **OTB-07: Biometric Bypass**
    * Hook `onAuthenticationSucceeded` via Frida. Login without fingerprint.
- [ ] **OTB-08: Step Skipping**
    * Force browse to `PaymentSuccess` activity directly.
- [ ] **OTB-09: GPS Spoofing**
    * Use "Fake GPS". Does the app validate location server-side?

---

## 5. Dynamic Analysis
*Runtime manipulation.*

- [ ] **DA-01: SSL Pinning Bypass**
    * Can traffic be intercepted using Frida/Objection?
- [ ] **DA-02: Method Hooking**
    * Hook crypto functions to view plain-text data.
- [ ] **DA-03: File System Access**
    * Access sandbox files at runtime using Objection.

---

## 6. Findings Summary

| ID | Finding Title | Severity | Status |
| :--- | :--- | :--- | :--- |
| | | | |
| | | | |

---
