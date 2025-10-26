---
title: 保存時に適切に保護されていない暗号鍵 (Cryptographic Keys Not Properly Protected at Rest)
id: MASWE-0014
alias: crypto-keys-not-protected-at-rest
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-STORAGE-1]
  masvs-v2: [MASVS-CRYPTO-2, MASVS-STORAGE-1]
  cwe: [312, 318, 321]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/hardcoded-cryptographic-secrets
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf
status: new
---

## 概要

暗号鍵はモバイルアプリケーションの機密データを保護するために不可欠です。しかし、これらの鍵が保存時に適切に保護されていない場合、簡単に侵害される可能性があります。この弱点は、暗号化されていない SharedPreferences、保護されていないファイルなどの安全でない場所に暗号鍵を保存したり、アプリケーションコード内にハードコードしたり、ソース管理システムやバージョン管理システムに含めることで最終的に本番のアプリケーションパッケージに組み込まれる可能性があることに起因します。

攻撃者はアプリを逆コンパイルやリバースエンジニアして、ハードコードされた鍵を抽出できます。

## 影響

- **不正アクセス**: 暗号鍵が適切に保護されていない場合、攻撃者は機密データに不正アクセスし、アイデンティティ窃取の可能性があります。
- **完全性の喪失**: 鍵が侵害されると、攻撃者は暗号化されたデータを改竄できる可能性があります。
- **機密性の喪失**: 機密情報がさらされると、機密性の喪失をもたらす可能性があります。鍵がさらされると、その鍵で暗号化されたすべてのデータが危険にさらされます。

## 流入の形態

- **Insecure Storage Locations**: Storing cryptographic keys in unencrypted SharedPreferences, unprotected files, or other insecure locations.
- **Hardcoded Keys**: Including cryptographic keys directly in the application code, making them susceptible to extraction through decompilation and reverse-engineering.
- **Lack of Encryption**: Exporting cryptographic keys in plain text without encrypting them using a secure method.

## 緩和策

- **Use Platform Keystores**: Where possible, generate cryptographic keys dynamically on the device, rather than using predefined keys, and ensure that they are securely stored after creation. For this you can use the platform-specific keystores, such as the [Android KeyStore](https://developer.android.com/training/articles/keystore) or [iOS KeyChain](https://developer.apple.com/documentation/security/keychain_services).
- **Implement Strongest Hardware Security Solutions**: For the most critical cases and whenever [available and compatible](https://developer.android.com/privacy-and-security/keystore#HardwareSecurityModule) for the use case at hand, leverage the strongest hardware-backed security options such as [Android StrongBox](https://source.android.com/docs/security/features/keystore/strongbox) or iOS's Secure Enclave [`kSecAttrTokenIDSecureEnclave`](https://developer.apple.com/documentation/security/ksecattrtokenidsecureenclave) option to ensure the highest protection including physical and side-channel attacks.
- **Use Cryptographic Key Management Systems**: Securely retrieve keys from server-side services that provide secure storage, access control, and auditing for sensitive data. For example, AWS Secrets Manager, Azure Key Vault, or Google Cloud Secret Manager are some popular managed secrets storage solutions. The app can securely retrieve the necessary secrets at runtime through secure, authenticated API calls.
- **Encrypt and Wrap Keys**: Whenever storing keys in platform keystores is not suitable for the use case or keys need to be exported, use envelope encryption (DEK+KEK) and key wrapping techniques as specified in [NIST.SP.800-175Br1 5.3.5](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf) to protect cryptographic keys before storing them.
- **Follow Standard Key Management Best Practices**: Implement proper key management practices, including key rotation and robust protection mechanisms for keys in storage as outlined in [NIST.SP.800-57pt1r5 6.2.2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf), ensuring availability, integrity, confidentiality, and proper association with usage, entities, and related information.
