---
title: プライベートストレージの場所に暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Private Storage Locations)
id: MASWE-0006
alias: data-unencrypted-private-storage
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-STORAGE-2]
  masvs-v2: [MASVS-STORAGE-1, MASVS-CRYPTO-2]
  mastg-v1: [MASTG-TEST-0052, MASTG-TEST-0001]
  cwe: [312, 313, 922]
refs:
  - https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files
status: new
---

## 概要

モバイルアプリは、アプリケーションサンドボックスなどのプライベートストレージロケーション内にローカルに機密データを保存する必要があることがあり、このデータは、たとえば、不正なファイルパーミッション、アプリの脆弱性、デバイスの脆弱性、またはデータバックアップメカニズムを介した露出のリスクがあります。

[機密データ](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04b-Mobile-App-Security-Testing.md#identifying-sensitive-data "Sensitive Data") には、個人を識別できる情報 (PII)、パスワード、暗号鍵、セッショントークンを含むことがあります。

## 影響

- **機密性の喪失**: 適切な条件下では、攻撃者がアプリケーションサンドボックス内に内部的に保存されている機密データを抽出し、機密性を喪失して、なりすましやアカウント乗っ取りなどのさらなる攻撃を可能にします。

## 流入の形態

- **Data Stored Unencrypted**: Sensitive data is written to the app's private data directory (sandbox) unencrypted.
- **Hardcoded Encryption Key**: Sensitive data is encrypted but the key is hardcoded inside the application.
- **Encryption Key Stored on Filesystem**: Sensitive data is encrypted but the key is stored alongside it or in another easily accessible location.
- **Encryption Used is Insufficient**: Sensitive data is encrypted but the encryption is not considered to be strong.

## 緩和策

- Avoid storing sensitive data locally if not required for application functionality to reduce the likelihood and impact of this weakness. For example keeping PII server-side, rendering it at time of use, and removing any cached data on logout.
- Store cryptographic keys exclusively using the platform's hardware-backed keystore solution, such as the Android Keystore or the iOS Keychain.
- For storing other files and preferences, use platform-provided features for encrypting data at rest or other techniques implementing envelope encryption with Data Encryption Keys (DEK) and Key Encryption Keys (KEK) or equivalent methods. For example, on Android, use [`EncryptedFile`](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile) or [`EncryptedSharedPreferences`](https://developer.android.com/reference/androidx/security/crypto/EncryptedSharedPreferences); on iOS, use [iOS Data Protection](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files).

!!! Warning

    The **Jetpack security crypto library**, including the `EncryptedFile` and  `EncryptedSharedPreferences` classes, has been [deprecated](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library). However, since an official replacement has not yet been released, we recommend using these classes until one is available.
