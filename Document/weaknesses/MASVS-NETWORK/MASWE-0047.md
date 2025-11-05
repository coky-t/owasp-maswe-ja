---
title: 安全でないアイデンティティのピン留め (Insecure Identity Pinning)
id: MASWE-0047
alias: insecure-pinning
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-NETWORK-4]
  masvs-v2: [MASVS-NETWORK-2]
  cwe: [295]
status: new
---

## 概要

[アイデンティティピン留め (別名、証明書ピン留め、公開鍵ピン留め、TLS ピン留め)](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04f-Testing-Network-Communication.md#restricting-trust-identity-pinning) は、モバイルアプリを証明書や公開鍵などの特定の暗号アイデンティティに関連付け、アプリが信頼できるサーバーとのみ通信するように確保することを指します。

モバイルアプリが証明書ピン留めを実装しない場合、または正しく実装されていない場合、アプリは [中間マシン (MITM)](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04f-Testing-Network-Communication.md#intercepting-network-traffic-through-mitm) 攻撃に脆弱なままとなり、攻撃者はアプリと意図したサーバー間の通信を傍受して改変することができます。これは、アプリが不正な証明書を提示され、アプリがそれを知らないうちに信頼してしまう場合に発生し、それによって機密データにアクセスしたり、データストリームに悪意のあるコンテンツを注入する可能性があります。

**制限事項**: 証明書ピン留めは、アプリが特定の事前定義された証明書または公開鍵を持つサーバーへの接続のみを受け入れるようにすることで、信頼性の検証レイヤを追加します。これは、信頼できる証明機関 (CA) が侵害された場合でも、不正な傍受のリスクを軽減します。ただし、これは確実ではありません。

- アプリをリバースエンジニアできる攻撃者は、事前定義された PIN や証明書ピン留めロジックを解析し、削除または改変して、そのチェックを恒久的にバイパスします。
- [改竄と実行時計装 (Tampering and Runtime Instrumentation)](https://github.com/coky-t/owasp-mastg-ja/blob/master/techniques/generic/MASTG-TECH-0051.md) 技法を実行できる攻撃者は、アプリを操作してピン留めチェックをバイパスします。

これは、高度な教に対するアプリの耐性を強化するために、**他のセキュリティ対策と併せて** 証明書ピン留めを実装することの重要性を浮き彫りにしています。

## 影響

- **Data Interception**: Attackers can capture and read sensitive information transmitted over the network.
- **Data Manipulation**: Attackers might alter data in transit, causing corruption or injecting malicious content.
- **Data Exposure**: Sensitive information can be compromised.
- **Denial of Service**: Incorrect pinning may cause legitimate connections to fail, leading to service disruptions for users. For example, if a pinned certificate expires and is not updated, the app may be unable to establish secure connections.

## 流入の形態

- **Improper Configuration of Pinning Libraries**: Misconfiguring libraries like TrustKit, OkHttp's `CertificatePinner`, Volley, or AFNetworking's `SSLPinningMode`, leading to ineffective pinning.
- **Dynamic Pinning without Security**: Retrieving pins dynamically over insecure channels without proper validation, making it easy for attackers to supply malicious pins.
- **Improper Validation Logic**: Custom pinning implementations that do not correctly validate the certificate chain or public key. For example, accepting any certificate that chains to a trusted root CA instead of a specific certificate or public key.
- **Lack of Backup Pins**: Not including backup pins to prevent connectivity issues if the primary pin is no longer valid.

## 緩和策

- **Prefer Platform-provided Solutions**: Use platform-provided mechanisms like Android's Network Security Configuration (NSC) or iOS's App Transport Security (ATS) to enforce pinning.
- **Use Trusted Pinning Libraries**: Refrain from writing custom pinning logic; instead, rely on established and well-maintained libraries and frameworks (e.g., TrustKit, OkHttp's `CertificatePinner`) and ensure they are correctly configured according to best practices.
- **Secure Dynamic Pinning**: If dynamic pinning is necessary, retrieve pins over secure channels and validate them thoroughly before use.
- **Pin to Public Keys Instead of Certificates**: Pin to the certificate's public key rather than the whole certificate to avoid issues regarding expiration and renewals.
- **Consistent Enforcement**: Apply pinning uniformly for all connections to servers that you control.
- **Regularly Update Pins**: Keep the pinned certificates or public keys up to date with the server's current configuration and have a process for updating the app when changes occur.
- **Implement Backup Pins**: Include backup pins (hashes of additional trusted public keys) to prevent connectivity issues if the primary key changes.
