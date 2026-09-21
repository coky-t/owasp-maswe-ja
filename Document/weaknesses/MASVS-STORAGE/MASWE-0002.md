---
title: プライベートストレージの外部に暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted Outside of Private Storage)
id: MASWE-0002
alias: data-unencrypted-shared-storage-no-user-interaction
requirement: "アプリはプライベートストレージの外部に保存される機密データを暗号化している。"
platform: [android, ios]
profiles: [L1, L2, EUDIW]
threat: MAS-THREAT-0002
attacks: [MAS-ATTACK-0010, MAS-ATTACK-0011]
mappings:
  masvs-v1: [MSTG-STORAGE-2]
  masvs-v2: [MASVS-STORAGE-1, MASVS-STORAGE-2]
  cwe: [200, 284, 312, 313, 732, 921, 922]
  android-risks:
  - sensitive-data-external-storage
  android-core-app-quality: [Sensitive_Data_Storage]
  maswe-beta: [MASWE-0007, MASWE-0002]
refs:
- https://developer.android.com/training/data-storage
- https://developer.android.com/privacy-and-security/security-tips#external-storage
---

## 概要

この脆弱性は、アプリが機密データを共有ストレージや外部ストレージに暗号化せずに保存し、ユーザーのやり取りなしで他のアプリがそれにアクセスできる場合に発生します。

Android では、アプリはアプリ固有の外部ストレージ (`getExternalFilesDir()`) に明示的にデータを保存し、`MediaStore`-API やストレージアクセスフレームワーク (SAF) を使用して共有フォルダにアクセスできます。アプリ固有の外部ストレージは他のアプリからはアクセスできません。しかし、外部ストレージが物理的な SD カードにある場合、それを取り外して読み取ることができます。外部ストレージがシステムによってエミュレートされている場合、アンロックされた端末にアクセスする人は _Android Debug Bridge (ADB)_ を使用してそれにアクセスできます。

この脆弱性は主に、共有ストレージや外部ストレージの明示的な使用を許可している、Android に関わるものです。一方で、iOS では外部フォルダを直接読み書きすることはできませんが、アプリはデフォルトでプリインストールされている Files アプリやドキュメントピッカーを使用して、システム全体で共有される場所への読み書きができます。

## 流入の形態

- **暗号化せずに保存されたデータ**: 機密データを暗号化せずに共有ストレージや外部ストレージに書き込みます。Android では、これにはアプリ固有の外部ストレージも含みます。
- **ハードコードされた暗号鍵**: 外部ストレージに保存する機密データを、アプリケーション内にハードコードされた鍵で暗号化します。
- **ファイルシステム上に保存された暗号鍵**: 外部ストレージに保存する機密データを暗号化しますが、鍵をそのそばやその他の容易にアクセスできる場所に保存します。
- **不十分な暗号化**: 強力とはみなされていないアルゴリズムや設定で機密データを暗号化します。
- **暗号鍵の再使用**: 単一ユーザーによって所有される二つのデバイス間で暗号鍵を共有し、外部ストレージを介してそれらのデバイス間でデータを複製できます。

## 影響

- **機密データの侵害**: 攻撃者は、個人情報や、写真、ドキュメント、音声ファイルなどのメディアを抽出して、ユーザーデータの不正な開示を招く恐れがあります。
- **認証または認可のバイパス**: 攻撃者はパスワード、暗号鍵、セッショントークンを抽出して、なりすましやアカウント乗っ取りにつながる恐れがあります。
- **保護メカニズムのバイパス**: 攻撃者は、プレミアム機能の状態を記述するデータベースなど、アプリで使用されるデータを改竄して、ビジネスロジックの回避やアプリ所有者の収益損失をもたらす恐れがあります。

## 緩和策

- **プライベートストレージを優先する**: 可能な限り [プライベートな内部ストレージ](https://developer.android.com/training/data-storage/app-specific#internal) にファイルを保存します。
- **プラットフォームのファイル共有を制限する**: 可能な限り Android の Storage Access Framework (SAF) や iOS のドキュメントピッカーといったプラットフォームのストレージ共有フレームワークを使用して機密データを共有することを禁止します。
- **書き込み前にデータを暗号化する**: 共有ストレージや外部ストレージに保存される機密データは [Android の `EncryptedFile` API](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile) などを使用して暗号化します。
- **暗号鍵を保護する**: データ暗号化で使用される鍵を、利用可能な場合にはデバイスのハードウェア支援のキーストアで保護します。決してアプリケーション内にハードコードしてはいけません。

> [!WARNING]
> 
> `EncryptedFile` クラスと `EncryptedSharedPreferences` クラスを含む **Jetpack Security Crypto ライブラリ** は [非推奨](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library) になりました。ただし、公式の代替品はまだリリースされていないため、それが利用可能になるまではこれらのクラスを使用することをお勧めします。
