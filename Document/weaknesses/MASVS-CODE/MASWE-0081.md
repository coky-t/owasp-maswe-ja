---
title: 外部インタフェースからのデータの安全でない取り扱い (Unsafe Handling Of Data From External Interfaces)
id: MASWE-0081
alias: unsafe-external-data
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-CODE-4]
  cwe: [924]

draft:
  description: When data is received from external interfaces (e.g. Bluetooth, NFC,
    etc.), it should be treated as untrusted.
  topics:
  - Bluetooth
  - NFC
status: placeholder

---
