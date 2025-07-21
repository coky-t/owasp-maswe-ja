---
title: 実装されていないルート/脱獄検出 (Root/Jailbreak Detection Not Implemented)
id: MASWE-0097
alias: root-jailbreak-detection
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-1]
  masvs-v2: [MASVS-RESILIENCE-1]
  cwe: [693]

draft:
  description: no root/jailbreak detection implemented e.g. check for Cydia, SuperSU,
    Magisk, Xposed, etc. The app does not implement effective techniques to detect if the device is rooted or jailbroken (CWE-693).
  topics:
  - detection in place
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---
