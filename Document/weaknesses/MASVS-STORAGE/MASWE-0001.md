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

- **機密データのローカル保存を最小限に抑える**: アプリ機能に必要とされない限り、機密データをローカルに保存することを避けます。たとえば、PII をサーバーサイドに保持し、使用時に描画し、ログアウト時にキャッシュされたデータを削除します。
- **ファイルアクセスを制限する**: プラットフォーム API を使用して、ファイルアクセスを可能な限り制限します (最小権限の原則)。Android では、非推奨の `MODE_WORLD_READABLE`/`MODE_WORLD_WRITEABLE` ファイルパーミッションモードではなく、個別のパーミッション付与で適切に設定された `ContentProvider`/ `FileProvider` を通じてデータを共有します。iOS では、実現可能な最も厳格なアクセスビリティ属性 (`kSecAttrAccessibleWhenUnlockedThisDeviceOnly` など) でキーチェーンアイテムを保存します。
- **不要になったデータを削除する**: 機密データ、キャッシュ、一時ファイルが不要になった際 (ログアウト時や機密性の高いフローを去る場合など) に直ちに削除し、露出する恐れのある期間を制限します。
- **プラットフォームキーストアを使用する**: Android キーストアや iOS キーチェーンなど、プラットフォームのハードウェア基盤のキーストアソリューションのみを使用して暗号鍵を保存します。
- **保存時にデータを暗号化する**: その他のファイルや設定には、プラットフォームが提供する保存時にデータを暗号化する機能や、Data Encryption Keys (DEK) と Key Encryption Keys (KEK) を用いてエンベロープ暗号化を実装するその他の技法、あるいは同等の手法を使用します。たとえば、Android では [`EncryptedFile`](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile) または [`EncryptedSharedPreferences`](https://developer.android.com/reference/androidx/security/crypto/EncryptedSharedPreferences) を使用し、iOS では [iOS データ保護](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files) を使用します。

> [!WARNING]
> 
> `EncryptedFile` クラスと `EncryptedSharedPreferences` クラスを含む **Jetpack Security Crypto ライブラリ** は [非推奨](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library) になりました。ただし、公式の代替品はまだリリースされていないため、それが利用可能になるまではこれらのクラスを使用することをお勧めします。
