---
title: 不適切な乱数生成 (Improper Random Number Generation)
id: MASWE-0027
alias: improper-random-number-generation
platform: ["android", "ios"]
profiles: ["L1", "L2"]
mappings:
  masvs-v1: [MSTG-CRYPTO-6]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [332, 337, 338]
  android-risks: 
  - https://developer.android.com/privacy-and-security/risks/weak-prng
observed_examples:
- https://nvd.nist.gov/vuln/detail/CVE-2013-6386
- https://nvd.nist.gov/vuln/detail/CVE-2013-6386
- https://nvd.nist.gov/vuln/detail/CVE-2006-3419
- https://nvd.nist.gov/vuln/detail/CVE-2008-4102
- https://www.zellic.io/blog/proton-dart-flutter-csprng-prng/
status: new
---

## 概要

A [pseudorandom number generator (PRNG)](https://en.wikipedia.org/wiki/Pseudorandom_number_generator) algorithm generates sequences based on a seed with insufficient entropy that may be predictable. Common implementations are not cryptographically secure. For example, they typically use a linear congruential formula, allowing an attacker to predict future outputs, given enough observed outputs. Therefore, it is not suitable for security-critical applications or protecting sensitive data.

## 影響

- **Bypass Protection Mechanism**: Using a non-cryptographically secure PRNG in a security context, such as authentication, poses significant risks. An attacker could potentially guess the generated numbers and gain access to privileged data or functionality. Predicting or regenerating random numbers can lead to encryption breaches, compromise sensitive user information, or enable user impersonation.

## 流入の形態

- **Risky Random APIs**: The app may use many existing APIs to generate random numbers with insufficient entropy.
- **Non-random Sources**: The app may use custom methods to create "supposedly random" values, using non-random sources such as the current time.

## 緩和策

For security-relevant contexts, use cryptographically secure random numbers.

In general, it is strongly recommended not to use any random function in a deterministic way, even if it's a secure one, especially those involving hardcoded seed values (which are vulnerable to exposure by decompilation).

Refer to the [RFC 1750 - Randomness Recommendations for Security](https://www.ietf.org/rfc/rfc1750.txt) and the [OWASP Cryptographic Storage Cheat Sheet - Secure Random Number Generation](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html#secure-random-number-generation) for more information and recommendations on random number generation.
