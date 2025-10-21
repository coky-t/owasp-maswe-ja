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

- **暗号化なしで保存されたデータ**: 機密データは暗号化なしでアプリのプライベートデータディレクトリ (サンドボックス) に書き込まれます。
- **ハードコードされた暗号鍵**: 機密データは暗号化されますが、鍵はアプリケーション内にハードコードされています。
- **ファイルシステムに保存された暗号鍵**: 機密データは暗号化されますが、鍵は近くまたは簡単にアクセスできる別の場所に保存されています。
- **使用される暗号が不十分**: 機密データは暗号化されますが、暗号は強力とはいえません。

## 緩和策

- アプリケーションの機能に必要でない場合は、機密データをローカルに保存することを避け、この弱点の発生可能性と影響を軽減します。たとえば、PII をサーバーサイドで保持し、使用時に提供し、ログアウト時にキャッシュされたデータを削除します。
- Android キーストアや iOS キーチェーンなど、プラットフォームのハードウェア基盤のキーストアソリューションのみを使用して暗号鍵を保存します。
- その他のファイルや設定を保存する場合は、プラットフォームが提供する保存時にデータを暗号化する機能や、Data Encryption Keys (DEK) と Key Encryption Keys (KEK) を用いてエンベロープ暗号化を実装するその他の技法、あるいは同等の手法を使用します。たとえば、Android では [`EncryptedFile`](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile) または [`EncryptedSharedPreferences`](https://developer.android.com/reference/androidx/security/crypto/EncryptedSharedPreferences) を使用し、iOS では [iOS データ保護](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/encrypting_your_app_s_files) を使用します。

### !!! 警告

`EncryptedFile` クラスと `EncryptedSharedPreferences` クラスを含む **Jetpack Security Crypto ライブラリ** は [非推奨](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library) になりました。ただし、公式の代替品はまだリリースされていないため、それが利用可能になるまではこれらのクラスを使用することをお勧めします。
