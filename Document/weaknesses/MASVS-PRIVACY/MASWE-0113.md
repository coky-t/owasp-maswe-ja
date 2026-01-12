---
title: 適切なデータ管理コントロールの欠如 (Lack of Proper Data Management Controls)
id: MASWE-0113
alias: data-management-controls
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-4]
  cwe: [359]
refs:
- https://developer.apple.com/app-store/app-privacy-details/#privacy-links
status: new
---

## 概要

モバイルアプリが個人データを管理することに特化して設計されたメカニズムをユーザーに提供しない場合、ユーザーは情報を管理するための適切な選択肢を失います。これは、ユーザーのデータに対する権利を制限し、プライバシーに関する懸念、潜在的なデータ侵害の深刻化、プライバシー規制の潜在的な不遵守につながります。

これらのメカニズムは一般的にユーザーがアプリインタフェース内で直接的に削除、エクスポート、変更、またはデータ収集のオプトアウトを行う機能を含みます。たとえば、あるアプリでは設定メニュー内にデータ管理機能を提供したり、別のものではユーザーがデータを管理できる外部ウェブサイトへのリンクを提供します。

## 流入の形態

- **適切なデータ管理設定の欠如**: ユーザーに削除、エクスポート、変更、データ収集のオプトアウトのための機能を提供しておらず、ユーザーが個人データを制限されたりまったく制御できなくなります。

## 影響

- **ユーザー権利の侵害**: ユーザーは、情報の削除やエクスポートなど、個人データを管理する権利を行使できず、制御の欠如とプライバシーリスクの増大につながる可能性があります。
- **プライバシー規制の不遵守**: GDPR や CCPA など、ユーザーにデータ管理機能を提供することを義務付ける規制に遵守しないと、罰金、法的措置、その他の結果につながる可能性があります。
- **ユーザーの信頼の喪失**: ユーザーは個人データを管理できないアプリへの信頼を失う可能性があり、否定的なレビュー、ユーザーエンゲージメントの低下、リテンションの低減につながる可能性があります。

## 緩和策

- **Implement Data Management Mechanisms**: Ensure that mechanisms are in place for users to delete, export, or modify their data. Provide granular controls for specific aspects of data collection and sharing (e.g., location services, contacts, media access).
- **Regularly Update Data Management Features**: Regularly review and update data management features to ensure compliance with evolving regulations and user expectations. This helps maintain transparency and user trust.
- **User-Friendly Data Management Interface**: Create a user-friendly interface for data management controls, ensuring that users can easily navigate and exercise their rights over their personal data without friction.
