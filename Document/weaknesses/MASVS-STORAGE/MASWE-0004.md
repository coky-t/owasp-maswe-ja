---
title: バックアップから除外されない機密データ (Sensitive Data Not Excluded From Backup)
id: MASWE-0004
alias: data-not-excluded-backup
platform: [android, ios]
profiles: [L1, L2, P]
mappings:
  masvs-v1: [MSTG-STORAGE-8]
  masvs-v2: [MASVS-STORAGE-2, MASVS-PRIVACY-1]
  cwe: [212]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/backup-best-practices

refs:
- https://developer.android.com/guide/topics/data/autobackup#include-exclude-android-11
- https://developer.android.com/guide/topics/data/autobackup#include-exclude-android-12
status: new

---

## 概要

iOS と Android はアプリデータを自動的にクラウドサービスにバックアップします。ユーザーは物理マシン上にローカルバックアップを作成することもできますし、スマートフォンを切り替える際のデータ転送時に自動的にバックアップが作成されます。開発者がアプリのバックアップ処理方法を適切に設定しておらず、機密ファイルを除外していない場合、バックアップには機密性の高いユーザーデータやアプリデータを含む可能性があります。特定の状況下では、クラウドプロバイダによってバックアップが適切に保護されていないことや、悪意のある人物がバックアップファイルを改竄し、アプリの動作を改変したり、機密情報を抽出する可能性があります。

## 影響

- **アプリの動作改変**: 攻撃者はバックアップ内のデータを改竄し、アプリのロジックを改変する可能性があります。たとえば、プレミアム機能の状態を追跡するデータベースを改竄し、改竄したバックアップをデバイスに復元することが可能です。他のよくあるシナリオとしては、ワンタイムクーポンを引き換える前にデバイスをバックアップし、引き換え後にバックアップを復元するものがあり、悪意のある人物が同じクーポンを複数回再使用できます。
- **機密性の喪失**: バックアップに保存されている機密データ (個人情報、写真、文書、音声ファイルなど) は攻撃者によって抽出され、プライバシー侵害につながる可能性があります。
- **認証マテリアルの漏洩**: 攻撃者はパスワード、暗号鍵、セッショントークンを抽出し、なりすまし、アカウント乗っ取り、不正アクセスなどのさらなる攻撃を容易にする可能性があります。

## 流入の形態

- **自動システムバックアップ**: デフォルトでは、初期設定時にユーザーが同意すると、iOA と Android はアプリデータをクラウドにバックアップします。
- **ローカルバックアップ**: ユーザーはデバイスをローカルシステム (ラップトップなど) にバックアップできます。ローカルバックアップが暗号化せずに保存されていたり、安全に扱われていないと、攻撃者がデータを改竄する可能性があります。
- **デバイス間転送**: デバイス間でデータを転送 (iCloud や Google のデバイス間移行ツールなどにより) すると、攻撃者が同様の攻撃を実行することを可能にします。

## 緩和策

- Android では `android:allowBackup` や `BackupAgent` の `excludeFromBackup` など、プラットフォーム固有の属性を使用して、バックアップから機密ファイルを除外します。iOS では、`NSURLIsExcludedFromBackupKey` などの API はバックアップからの除外を [保証しません](https://developer.apple.com/documentation/foundation/optimizing_your_app_s_data_for_icloud_backup/#3928527)。そのため、代わりにデータを暗号化する必要があります。
- Keychain や iOS の `Library/Caches` など、デフォルトでバックアップから除外される場所に機密データを保存します。
- 保存前に機密データを暗号化して、バックアップされた場合でも機密性を確保します。
