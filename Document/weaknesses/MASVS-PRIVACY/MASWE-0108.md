---
title: ネットワークトラフィックの機密データ (Sensitive Data in Network Traffic)
id: MASWE-0108
alias: sensitive-data-in-network-traffic
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: [MSTG-NETWORK-1]
  masvs-v2: [MASVS-PRIVACY-1]
  cwe: [359]
status: new
---

## 概要

ネットワークトラフィックの機密データは、認可されていないパーティによって傍受およびアクセスされる可能性のある方法でのネットワーク経由の個人情報や機密情報の送信を指します。データは HTTPS などの安全なプロトコルを使用して送信されることもありますが、共有または収集されるデータの適切性と必要性が最優先事項となります。

リスクは送信手法のセキュリティではなく、送信されるデータのプライバシーへの影響にあります。これは、ユーザーの個人情報、位置データ、使用パターン、その他のユーザープライバシーを侵害する可能性のある情報を含む可能性があります。

## 流入の形態

このリスクは以下のようなさまざまなシナリオでもたらされる可能性があります。

- アプリの機能要件を超えるユーザーデータの過剰な収集。
- 適切な匿名化なしで、詳細なユーザー位置情報や行動分析の送信。
- ユーザーの同意なしで、サードパーティサービス (アナリティクス、広告ネットワークなど) と機密情報の共有。
- IMEI、電子メール、電話番号などの識別子の不必要な収集。

## 影響

ネットワークトラフィックの機密データ露出の影響には以下があります。

- **ユーザープライバシーの侵害**: ユーザーは個人情報が送信されていることに気付かず、プライバシー侵害につながる可能性があります。
- **コンプライアンスおよび法的リスク**: データ保護の法律や規制 (GDPR など) に違反し、法的措置や罰金につながります。
- **ユーザー信頼の喪失**: ユーザーはアプリケーションへの信頼を失い、評判の低下やビジネス損失につながる可能性があります。

## 緩和策

To mitigate this risk, consider the following strategies:

- Minimize the collection of user data to what is strictly necessary for app functionality.
- Implement and strictly enforce data privacy policies, including user consent for data collection and sharing.
- Use anonymization techniques for user data that is transmitted for analytics or other secondary purposes.
- Regularly review and audit data transmitted over the network to ensure it aligns with privacy policies and user expectations.
- Provide clear user-facing privacy settings, allowing users to control what data is shared.
