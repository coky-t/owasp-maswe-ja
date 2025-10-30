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

- **破られたアルゴリズム**: RC4 などの破られた暗号アルゴリズム (つまり、NIST や他の標準で非推奨または禁止されているもの) に依存しています。
- **リスクのあるアルゴリズム構成**: 不十分なエントロピーの IV を使用したり、AES-CBC や AES-CTR などのモードで再使用すると、セマンティックセキュリティを損ない、攻撃者がパターンを検出したり、平文の差分を復元できるようになります。AES-GCM などの AEAD モードでは、ノンスの再使用や不十分な長さの認証タグを使用することで、機密性と完全性の両方を損ないます。
- **破られた動作モード**: 破られたとみなされるモードを使用しています。たとえば、AES-ECB は実用的な既知平文攻撃により破られており、NIST によって禁止されています。
- **不十分な鍵長**: 不十分な鍵サイズ (AES で 128 ビット鍵など) を使用すると暗号強度を損ない、その暗号はブルートフォース攻撃の影響を受けやすくなります。
- **非暗号操作**: セキュリティ上の理由から、XOR、Base64 エンコーディング、単純な難読化手法などの技法に依存しています。これらの手法は実際の暗号化を提供せず、簡単に復元またはデコードされ、機密データをさらす可能性があります。

## 緩和策

- **Use Secure Encryption Modes**: Choose secure modes (e.g. approved by NIST) such as `AES/GCM/NoPadding`.
- **Ensure Proper Initialization Vector Management**: Generate IVs using cryptographically secure random number generators (with sufficient entropy) and ensure they are unique for every operation.
- **Use Sufficiently Long Keys**: Enforce sufficiently long keys such as those approved by NIST, e.g., a minimum of 256 bits for AES.
- **Rely on Proper Cryptographic Primitives**: Rely on well-vetted cryptographic primitives that have undergone rigorous peer review and formal validation.
