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

- **きめ細かなプライバシー設定の欠如**: 位置情報サービス、連絡先、メディアアクセスなど、データ収集と共有の特定の側面をユーザーが制御できるほどの十分にきめ細かいプライバシー設定を提供していない。この制御の欠如はユーザーがどの種類の情報を誰と共有するかを決定できないことにつながります。

## 影響

- **個人データの露出**: ユーザーは、電子メールアドレス、生年月日、オンラインステータスなどの機密情報を、同意なしに他者に意図せず露出する可能性があり、ハラスメントやアイデンティティ窃取のリスクを高めます。
- **プライバシー規制への非遵守**: 十分なプライバシーコントロールを提供していないアプリは、データの可視化と共有に関するユーザー制御を求める、GDPR や CCPA などの規制への非遵守問題に直面する可能性があります。
- **ユーザーの信頼の喪失**: ユーザーは、どの情報が誰と共有されるかについて十分な制御をできていないと感じると、アプリへの信頼を失い、否定的なレビューやアプリのエンゲージメントの低下につながる可能性があります。

## 緩和策

- **Offer Granular Privacy Settings**: Provide privacy settings with sufficient granularity, allowing users to control individual data collection categories (e.g., location, contacts) and manage their sharing preferences. Allow users to choose what information is visible to others, such as connection status or discoverability.
- **User Education on Privacy Options**: Clearly inform users about available privacy settings and how to use them effectively to manage data visibility. This can be done through tutorials, help sections, or contextual tips within the app.
- **Default Privacy-Friendly Settings**: Set default privacy settings to the most restrictive options, allowing users to opt-in to sharing specific information rather than having to opt-out, which helps to ensure user privacy by default.
