---
title: 使用されていないコンパイラ提供のセキュリティ機能 (Compiler Provided Security Features Not Used)
id: MASWE-0116
alias: compiler-provided-security-features-not-implemented
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-3, MASVS-CODE-4]
  cwe: [693]
refs:
- https://cs.android.com/android/platform/superproject/main/+/main:bionic/linker/linker_main.cpp;l=397?q=linker_main&ss=android%2Fplatform%2Fsuperproject%2Fmain
- https://partners.trellix.com/enterprise/en-us/assets/white-papers/wp-secure-coding-android-applications.pdf
- https://mas.owasp.org/MASTG/0x05i-Testing-Code-Quality-and-Build-Settings/#binary-protection-mechanisms
- https://mas.owasp.org/MASTG/0x06i-Testing-Code-Quality-and-Build-Settings/#binary-protection-mechanisms
- https://sensepost.com/blog/2021/on-ios-binary-protections/
- https://www.sans.org/blog/stack-canaries-gingerly-sidestepping-the-cage/
draft:
  description: The app is compiled without enabling memory protection mechanisms such as stack canaries, address space layout randomization (ASLR), non-executable memory, or position-independent executables (PIE), reducing resistance to memory corruption attacks (CWE-693).
  topics:
  - PIC
  - stack canaries
  note: PIC cannot be switched off in newer versions of Android, the NDK does not link against such libraries anymore [source](https://cs.android.com/android/platform/superproject/main/+/main:bionic/linker/linker_main.cpp;l=397?q=linker_main&ss=android%2Fplatform%2Fsuperproject%2Fmain). Alternative title could be Memory Anti-Exploitation Mechanisms Not Implemented.
status: placeholder
observed_examples:
- https://nvd.nist.gov/vuln/detail/CVE-2019-3568
---
