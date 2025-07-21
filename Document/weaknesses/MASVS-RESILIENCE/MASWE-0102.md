---
title: 実装されていない動的解析ツール検出 (Dynamic Analysis Tools Detection Not Implemented)
id: MASWE-0102
alias: dynamic-analysis-tools
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-4]
  masvs-v2: [MASVS-RESILIENCE-4]
  cwe: [693]

draft:
  description: The app's code doesn’t implement effective techniques to detect if it is being analyzed by dynamic analysis tools (CWE-693), e.g. Frida, Xposed, Ellekit, etc.
  topics:
  - Frida detection
  - Xposed detection
  - ElleKit detection
status: placeholder

---
