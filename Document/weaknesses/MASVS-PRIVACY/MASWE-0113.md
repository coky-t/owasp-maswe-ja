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

- **Violation of User Rights**: Users may be unable to exercise their rights to manage their personal data, such as deleting or exporting their information, leading to a lack of control and increased privacy risks.
- **Non-Compliance with Privacy Regulations**: Non-compliance with regulations like GDPR and CCPA, which require providing users with data management capabilities, can result in fines, legal action, and other consequences.
- **Loss of User Trust**: Users may lose trust in an app that does not allow them to manage their personal data, which can lead to negative reviews, decreased user engagement, and reduced retention.

## 緩和策

- **Implement Data Management Mechanisms**: Ensure that mechanisms are in place for users to delete, export, or modify their data. Provide granular controls for specific aspects of data collection and sharing (e.g., location services, contacts, media access).
- **Regularly Update Data Management Features**: Regularly review and update data management features to ensure compliance with evolving regulations and user expectations. This helps maintain transparency and user trust.
- **User-Friendly Data Management Interface**: Create a user-friendly interface for data management controls, ensuring that users can easily navigate and exercise their rights over their personal data without friction.
