---
title: 不適切な暗号化 (Improper Encryption)
id: MASWE-0020
alias: weak-encryption
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [326]

refs:
- https://support.google.com/faqs/answer/10046138?hl=en
- https://support.google.com/faqs/answer/9450925?hl=en
- https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf

status: new

---

## 概要

不適切な暗号化は、認可されていない個人が保護されたデータを復号できる、攻撃に対して脆弱な暗号システムや実装を指します。

## 影響

- **機密性の喪失**: 不適切な暗号化は、攻撃者が機密情報を解読して入手でき、不正な開示やデータ侵害につながる可能性があります。
- **完全性の喪失**: 不適切な暗号化はデータの完全性を損ない、攻撃者が検出されずに情報を改竄や操作できるようになります。

## 流入の形態

- **Broken Algorithms**: Relying on broken encryption algorithms (i.e., that are deprecated or disallowed by NIST or other standards) such as RC4.
- **Risky Algorithm Configurations**: Using IVs with insufficient entropy or reusing them in modes like AES-CBC or AES-CTR breaks semantic security, allowing attackers to detect patterns or recover plaintext differences. In AEAD modes like AES-GCM, reusing nonces or using authentication tags of insufficient length compromises both confidentiality and integrity.
- **Broken Modes of Operation**: Using modes that are considered broken. For example, AES-ECB is broken due to practical known-plaintext attacks and it's disallowed by NIST.
- **Insufficient Key Length**: The use of insufficient key sizes (e.g., 128-bit keys in AES) can compromise encryption strength making the encryption susceptible to brute-force attacks.
- **Non-Cryptographic Operations**: Relying on techniques such as XOR, Base64 encoding, or simple obfuscation methods for security purposes. These methods provide no actual encryption and can be easily reversed or decoded, exposing sensitive data.

## 緩和策

- **Use Secure Encryption Modes**: Choose secure modes (e.g. approved by NIST) such as `AES/GCM/NoPadding`.
- **Ensure Proper Initialization Vector Management**: Generate IVs using cryptographically secure random number generators (with sufficient entropy) and ensure they are unique for every operation.
- **Use Sufficiently Long Keys**: Enforce sufficiently long keys such as those approved by NIST, e.g., a minimum of 256 bits for AES.
- **Rely on Proper Cryptographic Primitives**: Rely on well-vetted cryptographic primitives that have undergone rigorous peer review and formal validation.
