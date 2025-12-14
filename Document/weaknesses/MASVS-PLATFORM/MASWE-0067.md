---
title: 無効化されていないデバッグフラグ (Debuggable Flag Not Disabled)
id: MASWE-0067
alias: debuggable-flag
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-2]
  masvs-v2: [MASVS-RESILIENCE-4]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/android-debuggable
  cwe: [489]

refs:
- https://developer.android.com/guide/topics/manifest/application-element
status: new
---

## 概要

モバイルアプリは一般的にアプリがデバッグ可能かどうかを決定する設定フラグを含みます。このフラグは開発時には不可欠ですが、本番で有効なままにすると深刻なセキュリティリスクをもたらす可能性があります。デバッグ可能なアプリは、ルート化していないデバイスや脱獄していないデバイスであっても、攻撃者がデバッガをアタッチし、メモリを検査し、実行フローを操作し、クライアントサイドコントロールをバイパスすることを可能にします。また、詳細なログ記録や開発者ツールを通じてアクセス可能な機密情報を露出する可能性もあります。

## 影響

- **Read and Modify Memory**: Attackers can read and modify the app's memory space, which can lead to the exposure of sensitive information, such as encryption keys, API keys, user credentials, or tokens that otherwise would be inaccessible since they aren't present in the app's code or stored to disk.
- **Bypassing Security Controls**: Attackers can bypass security controls, such as authentication and authorization mechanisms, by manipulating the app's execution flow.
- **Execute Unauthorized Code**: Attackers can inject and execute arbitrary code within the app's context, leading to further exploitation of the device or the app's data. For example, attackers can inject reverse engineering tools like Frida into the app even on non-rooted or non-jailbroken devices.
- **Access to Sensitive Logs**: Attackers can access logs that may contain sensitive information, such as user credentials, API keys, or other sensitive data that would otherwise be inaccessible. This can lead to further exploitation of the app or the device.

## 流入の形態

- **Misconfigured Build Settings**: Misconfigured build settings can accidentally leave an app in a state that is debuggable, exposing it to security vulnerabilities. This can result from improper selection of build variants, errors in CI/CD configurations, or mistakenly applying debug settings to production environments.

## 緩和策

- Ensure that the debuggable flag in the app's configuration file is not enabled for production builds. For example, by using build variants or flavours to separate debug and release configurations, ensure that the debuggable flag is enabled only for debug builds.
