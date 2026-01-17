---
title: 不十分なデータ可視性コントロール (Inadequate Data Visibility Controls)
id: MASWE-0114
alias: data-visibility-control
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-4]
  cwe: [359]
refs:
- https://firebase.google.com/support/privacy/storing-privacy-settings
- https://www.researchgate.net/publication/335863205_Demystifying_Hidden_Privacy_Settings_in_Mobile_Apps
status: new
---

## 概要

個人情報が他のユーザーやより広範な環境にどのように共有されるかを、モバイルアプリがユーザーに十分に制御を与えない場合、ユーザーは意図せず機密データを開示し、プライバシーの懸念や他のユーザーやサードパーティから望ましくない注目につながる可能性があります。このような情報の例には、最終接続ステータス、既読通知、生年月日、電子メールアドレス、検出設定などがあります。

ユーザーがデータの可視性を制御するための明確できめ細かなオプションを、一般的にアプリ設定の形で、利用できるようにすることは、ユーザのプライバシーを維持し、アプリへの信頼を築く上で非常に重要です。

## 流入の形態

- **Lack of Granular Privacy Settings**: Failing to provide privacy settings with sufficient granularity to allow users to control specific aspects of data collection and sharing, such as differentiating between location services, contacts, or media access. This lack of control results in users being unable to decide which types of information are shared and with whom.

## 影響

- **Exposure of Personal Data**: Users may unintentionally expose personal information, such as their email address, birthday, or online status, to others without their consent, increasing the risk of harassment or identity theft.
- **Non-Compliance with Privacy Regulations**: Apps that do not offer sufficient privacy controls may face non-compliance issues with regulations like GDPR or CCPA, which require user control over data visibility and sharing.
- **Loss of User Trust**: Users may lose trust in the app if they feel they have inadequate control over what information is shared and with whom, leading to negative reviews and decreased app engagement.

## 緩和策

- **Offer Granular Privacy Settings**: Provide privacy settings with sufficient granularity, allowing users to control individual data collection categories (e.g., location, contacts) and manage their sharing preferences. Allow users to choose what information is visible to others, such as connection status or discoverability.
- **User Education on Privacy Options**: Clearly inform users about available privacy settings and how to use them effectively to manage data visibility. This can be done through tutorials, help sections, or contextual tips within the app.
- **Default Privacy-Friendly Settings**: Set default privacy settings to the most restrictive options, allowing users to opt-in to sharing specific information rather than having to opt-out, which helps to ensure user privacy by default.
