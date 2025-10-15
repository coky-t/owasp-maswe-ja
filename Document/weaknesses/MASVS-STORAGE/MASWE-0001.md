---
title: 機密データのログへの挿入 (Insertion of Sensitive Data into Logs)
id: MASWE-0001
alias: data-in-logs
platform: ["android", "ios"]
profiles: ["L1", "L2", "P"]
mappings:
  masvs-v1: [MSTG-STORAGE-7]
  masvs-v2: [MASVS-STORAGE-2, MASVS-PRIVACY-1]
  cwe: [209, 359, 497, 532]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/log-info-disclosure
refs:
  - https://stackoverflow.com/questions/45270547/is-read-logs-a-normal-or-dangerous-android-permission
status: new
---

## 概要

モバイルアプリはログに [機密データ](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04b-Mobile-App-Security-Testing.md#identifying-sensitive-data "Sensitive Data") を書き込むことがあります。これは、パスワード、クレジットカード番号、その他の個人を識別できる情報 (PII) などの機密ユーザーデータや、暗号鍵、セッショントークン、その他の機密情報などの機密システムデータを含むことがあります。

開発時、特にアプリのデバッグには、あらゆる情報をログ記録することが非常に役立ちます。しかし、本番環境では必ずしも必要ではなく、潜在的な攻撃者に誤って開示することを避けるために、可能な限り防ぐ必要があります。

## 流入の形態

これは一般的に以下の二つの方法で発生します。

- **システムログ**: アプリケーションはシステムログに機密データをログ記録することがあり、デバイス (古い OS バージョン、侵害されたデバイス、または適切なパーミッションを持つもの) 上の他のアプリケーションからアクセスできます。
- **アプリログ**: アプリケーションはアプリケーションのデータディレクトリのファイルに機密データをログ記録することがあり、デバイスがルート化されている場合、デバイス上の任意のアプリケーションからアクセスできます。

## 影響

Loss of confidentiality: Sensitive data within logs is at risk of being exposed to an attacker with access to the device who may be able to extract it. This may lead to further attacks, such as identity theft, or compromise of the application's backend.

## 緩和策

The following are generic recommendations to avoid logging sensitive data in production releases:

- Avoid logging sensitive data at all.
- Redact sensitive data in logs.
- Remove logging statements unless deemed necessary to the application or explicitly identified as safe, e.g. as a result of a security audit.
- Use log levels properly to ensure that sensitive data is not logged in production releases.
- Use flags to disable logging in production releases.

The documentation for each platform provides best practices for developers:

- [Android mitigations to avoid log disclosure](https://developer.android.com/privacy-and-security/risks/log-info-disclosure#mitigations)
- [iOS mitigations to avoid log disclosure](https://developer.apple.com/documentation/os/logging/generating_log_messages_from_your_code#3665948)
