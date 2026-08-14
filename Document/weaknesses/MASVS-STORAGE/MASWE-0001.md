---
title: プライベートストレージに暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Private Storage)
id: MASWE-0001
alias: data-unencrypted-private-storage
requirement: "アプリはプライベートストレージに保存される機密データを暗号化している。"
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0001
attacks: [MAS-ATTACK-0005, MAS-ATTACK-0007, MAS-ATTACK-0008]
mappings:
  masvs-v1: [MSTG-STORAGE-2]
  masvs-v2: [MASVS-STORAGE-1, MASVS-STORAGE-2, MASVS-CRYPTO-2]
  cwe: [200, 284, 312, 313, 732, 922]
  android-risks:
  - file-providers
  maswe-beta: [MASWE-0006, MASWE-0002, MASWE-0118]
refs:
- https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files
- https://developer.android.com/about/versions/nougat/android-7.0-changes#permfilesys
- https://developer.android.com/privacy-and-security/security-tips#internal-storage
---

## 概要

この脆弱性は、アプリが機密データを暗号化せずに、アプリケーションサンドボックスなどのプライベートストレージの場所に保存する場合に発生します。不適切なファイルパーミッション、アプリやデバイスの脆弱性、データバックアップメカニズムを介して露出する恐れ場あります。

機密データには、個人を識別できる情報 (PII)、パスワード、暗号鍵、セッショントークンを含むことがあります。

## 流入の形態

- **暗号化なしで保存されたデータ**: 機密データを暗号化なしでアプリのプライベートデータディレクトリ (サンドボックス) に書き込みます。
- **ハードコードされた暗号鍵**: 機密データをアプリケーション内にハードコードされた鍵で暗号化します。
- **ファイルシステム上に保存された暗号鍵**: 機密データを暗号化しますが、生成鍵は近くまたは簡単にアクセスできる別の場所に保存します。
- **不十分な暗号化**: 機密データを強いとはみなされないアルゴリズムや設定で暗号化します。
- **不十分なアクセス制限**: プライベートファイルを、不適切なファイルパーミッション (Android で非推奨の `MODE_WORLD_READABLE`/`MODE_WORLD_WRITEABLE` ファイルパーミッションモードなど)、設定不備のある `FileProvider`、あるいは iOS で弱いアクセシビリティ属性 (`kSecAttrAccessibleAlways` など) で保護されたキーチェーンアイテムを通じて、他のアプリに露出します。
- **使用後に削除されないデータ**: 機密データをプライベートストレージ (キャッシュ、一時ファイル、WebView ステート、ネットワークキャッシュを含む) に必要以上に長く保持します。

## 影響

- **機密データの侵害**: 攻撃者はアプリケーションサンドボックスから PII やその他のユーザーデータを抽出し、不正な開示につながり、なりすましなどのさらなる攻撃を可能にします。
- **認証や認可のバイパス**: 攻撃者はパスワード、暗号鍵、またはセッショントークンを抽出でき、アカウント乗っ取りや保護された機能への不正アクセスにつながります。

## 緩和策

- **Minimize Local Storage of Sensitive Data**: Avoid storing sensitive data locally if it is not required for app functionality, e.g. keep PII server-side, render it at time of use, and remove any cached data on logout.
- **Restrict File Access**: Use platform APIs to restrict file access as much as possible (least privilege principle). On Android, share data through a properly configured `ContentProvider`/ `FileProvider` with per-grant permissions instead of the deprecated `MODE_WORLD_READABLE`/`MODE_WORLD_WRITEABLE` file permission modes. On iOS, store Keychain items with the strictest viable accessibility attribute (e.g. `kSecAttrAccessibleWhenUnlockedThisDeviceOnly`).
- **Remove Data When No Longer Needed**: Clear sensitive data, caches, and temporary files as soon as they are no longer needed (e.g. on logout or when leaving a sensitive flow) to limit the window during which they can be exposed.
- **Use Platform Keystores**: Store cryptographic keys exclusively using the platform's hardware-backed keystore solution, such as the Android Keystore or the iOS Keychain.
- **Encrypt Data at Rest**: For other files and preferences, use platform-provided features for encrypting data at rest or techniques implementing envelope encryption with Data Encryption Keys (DEK) and Key Encryption Keys (KEK) or equivalent methods. For example, on Android, use [`EncryptedFile`](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile) or [`EncryptedSharedPreferences`](https://developer.android.com/reference/androidx/security/crypto/EncryptedSharedPreferences); on iOS, use [iOS Data Protection](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files).

> [!WARNING]
> 
> `EncryptedFile` クラスと `EncryptedSharedPreferences` クラスを含む **Jetpack Security Crypto ライブラリ** は [非推奨](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library) になりました。ただし、公式の代替品はまだリリースされていないため、それが利用可能になるまではこれらのクラスを使用することをお勧めします。
