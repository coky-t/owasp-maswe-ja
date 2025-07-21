---
title: 不適切な暗号鍵生成 (Improper Cryptographic Key Generation)
id: MASWE-0009
alias: weak-crypto-key-generation
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2]
  masvs-v2: [MASVS-CRYPTO-2]
  cwe: [331, 337, 338]
  android-risks: 
    - https://developer.android.com/privacy-and-security/risks/weak-prng
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://developer.android.com/privacy-and-security/cryptography
- https://developer.android.com/reference/javax/crypto/KeyGenerator

status: new
---

## 概要

In cryptography, the security strength is heavily influenced by the methods used to generate cryptographic keys. One critical aspect is the key size, also known as the key length, which is measured in bits and must comply with the latest security best practices. Encryption algorithms that use insufficient key sizes are vulnerable to attack, while longer keys typically result in more complex encryption.

However, even with a sufficiently large key size, the security of the encryption can be compromised if the key generation process is flawed. Failing to use strong, cryptographically secure pseudorandom number generators (CSPRNGs) with sufficient entropy can generate predictable keys that are easier for attackers to guess or reproduce and that are susceptible to repetitive patterns.

## 影響

- **Risk of Brute-Force Attacks**: Improper key generation, whether due to shorter key length or predictable random number generator (PRNG) inputs, increases the risk of brute-force attacks. Attackers can more easily guess or systematically try possible keys until they find the correct one.
- **Loss of Confidentiality**: Encryption relies on strong keys to maintain the confidentiality of sensitive data. Seed values with insufficient entropy can allow attackers to decrypt and access confidential information, leading to unauthorized disclosure and potential data breaches.
- **Loss of Integrity**: Improper key generation can compromise data integrity, allowing attackers to exploit vulnerabilities and potentially alter or tamper with the information without detection.

## 流入の形態

- **Insufficient Entropy**: Using a source of randomness with insufficient entropy can lead to predictable cryptographic keys.
- **Insufficient Key Length**: Cryptographic keys that are too short provide inadequate security. For example, keys shorter than recommended lengths for modern algorithms may be vulnerable to brute force attacks, making them easier for attackers to break.
- **Using Risky or Broken Algorithms**: Relying on deprecated, risky or inherently broken cryptographic algorithms can result in the generation of weaker keys. As these algorithms often have vulnerabilities or support shorter key lengths, they are more susceptible to modern attacks, compromising the overall security of the app.

## 緩和策

- Always use modern, well-established cryptographic libraries and APIs that follow best practices for entropy generation and key management.
- Ensure that key lengths meet or exceed current standards for cryptographic security, such as 256-bit for AES encryption and 2048-bit for RSA (considering quantum computing attacks). See ["NIST Special Publication 800-57: Recommendation for Key Management: Part 1 – General"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf) and ["NIST Special Publication 800-131A: Transitioning the Use of Cryptographic Algorithms and Key Lengths"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf) and ["BlueKrypt's Cryptographic Key Length Recommendation"](https://www.keylength.com/) for more information on cryptographic key sizes.
