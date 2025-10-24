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

暗号において、セキュリティの強度は暗号鍵を生成するために使用される手法に大きく影響を受けます。重要な側面の一つは鍵サイズ (鍵長とも呼ばれます) であり、ビット単位で測定され、最新のセキュリティベストプラクティスに準拠する必要があります。不十分な鍵サイズを使用する暗号アルゴリズムは攻撃に脆弱であり、鍵が長いほど一般的により複雑な暗号になります。

しかし、鍵サイズが十分に大きくても、鍵生成プロセスに欠陥があれば暗号のセキュリティが侵害される可能性があります。十分なエントロピーを持つ強力で暗号論的にセキュアな擬似乱数生成器 (CSPRNG) を使用しないと、攻撃者が推測したり再現しやすく、繰り返しパターンの影響を受けやすい、予測可能な鍵を生成する可能性があります。

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
