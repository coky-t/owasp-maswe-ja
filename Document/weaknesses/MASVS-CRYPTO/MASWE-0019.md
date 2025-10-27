---
title: リスクのある暗号実装 (Risky Cryptography Implementations)
id: MASWE-0019
alias: potentially-weak-crypto-impl
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2]
  masvs-v2: [MASVS-CRYPTO-1, MASVS-CODE-3]
  mastg-v1: [MASTG-TEST-0061, MASTG-TEST-0014]
  cwe: [326, 327, 1240]

refs: 
 - https://book.hacktricks.xyz/crypto-and-stego/cryptographic-algorithms
 - https://eudl.eu/pdf/10.4108/eai.3-12-2015.2262471
 - https://www.scitepress.org/papers/2014/50563/50563.pdf
 - https://pure.tugraz.at/ws/portalfiles/portal/23858147/main.pdf
 - https://github.com/Wind-River/crypto-detector
 - https://github.com/Rami114/cryptoscan/
 - https://github.com/IAIK/CryptoSlice
 - https://developer.android.com/reference/javax/crypto/Cipher#getInstance(java.lang.String)
 - https://developer.android.com/privacy-and-security/security-gms-provider
 - https://developer.android.com/privacy-and-security/cryptography#bc-algorithms
 - https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library
 - https://developer.android.com/privacy-and-security/cryptography#crypto_provider
 - https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
 - https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile
---

## 概要

リスクのある暗号実装、または、FIPS 140-2/3 (Federal Information Processing Standards) などの確立されたセキュリティ標準を満たしていないものなどの非準拠の暗号実装は、十分にテストされていないアルゴリズムや認定を受けていないアルゴリズムを使用する可能性があり、安全な鍵管理のベストプラクティスに従っていない可能性があり、厳密なピアレビューや形式検証を受けていないカスタム暗号ソリューションを含む可能性があります。

## 影響

確立された標準に従わずに作成されたカスタム暗号実装はブルートフォースや差分暗号解析などの攻撃の影響を受けやすくなります。さらに、暗号を正しく実装することは非常に困難であり、正しくないパディングや欠陥のある乱数生成といった、カスタムソリューションの小さなエラーでさえ、システムのセキュリティを完全に弱体化する可能性があり、攻撃者に機密データをさらす可能性があります。

そのような欠陥に伴う影響は非常に広範に及ぶ可能性があり、予測や測定が困難になります。

- **データ侵害**: リスクのある暗号実装は機密データの不正アクセスにつながり、データ侵害をもたらす可能性があります。
- **機密性、完全性、真正性の侵害**: 暗号の主要な原則 (機密性、完全性、真正性) が侵害されます。攻撃者は、正当なユーザーやシステムを復号、操作、なりすますことが可能です。

## 流入の形態

- **Deviation from standard libraries**: Not using well-known libraries for cryptography, such as those provided by the platforms like Conscrypt or CryptoKit, or other well-established libraries like OpenSSL, BouncyCastle, etc.
- **Use of cryptographic constants**: Hardcoded cryptographic constants are typically used to implement cryptographic algorithms. These constants include S-boxes (substitution boxes) for block ciphers, permutation tables, etc.
- **Use of low-level mathematical operations**: Low-level mathematical operations (such as bitwise operations, shifts, custom padding schemes) typically used in cryptographic algorithms.
- **High entropy code**: An indicator of cryptographic implementations or heavily obfuscated code that may hide cryptographic algorithms from reverse engineering.
- **Use of non-cryptographic functions**: Non-cryptographic functions such as Base64 encoding or XOR instead of encryption.

## 緩和策

- **Use standard cryptographic libraries and avoid custom cryptography**: Avoid developing custom cryptographic algorithms or protocols. Always prefer well-established and widely accepted cryptographic libraries such as OpenSSL, BoringSSL, or platform-specific libraries such as Android's Conscrypt and Apple's CryptoKit. These libraries have undergone extensive testing and are regularly updated to address new security threats.

- **Ensure compliance with security standards**: If you can't avoid using custom cryptography, make sure it's implemented to meet industry standards such as FIPS 140-2/3 (Federal Information Processing Standards) or the latest National Institute of Standards and Technology (NIST) recommendations.
- **Perform periodic security audits**: If using custom cryptography is unavoidable, perform regular security audits (including thorough code reviews) to identify and remediate any flaws in your custom cryptographic implementations. Engage external security experts to provide an unbiased assessment.
