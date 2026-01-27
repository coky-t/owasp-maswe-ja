---
title: 不十分なパーミッション管理 (Inadequate Permission Management)
id: MASWE-0117
alias: inadequate-permission-management
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-1]
  cwe: [250]
refs:
- https://developer.apple.com/design/human-interface-guidelines/privacy#Requesting-permission
- https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources
- https://developer.android.com/training/permissions/requesting
- https://support.google.com/googleplay/android-developer/answer/9888170?hl=en
- https://developer.android.com/privacy-and-security/minimize-permission-requests
- https://developer.android.com/training/permissions/usage-notes
- https://arxiv.org/pdf/1905.02713
- https://arxiv.org/pdf/2203.10583
- https://ieeexplore.ieee.org/document/9001128
- https://www.enisa.europa.eu/sites/default/files/publications/WP2017%20O-2-2-4%20GDPR%20Mobile.pdf

status: new
---

## 概要

パーミッションは、カメラ、マイク、位置情報、ストレージといった機密性の高いデバイス機能へのアクセスを制御し、モバイルアプリプライバシーの重要な側面となります。パーミッションはデータ収集と処理の関門として機能するため、適切なパーミッション管理は、ユーザープライバシーを保護し、規制を遵守するために不可欠です。

### ファーストパーティアプリ

ファーストパーティアプリは必要以上に多くのパーミッションを要求することがあり、認識不足、技術的制約、ビジネスニーズによりプライバシーに配慮した代替策を見落とすことがよくあります。開発者は機能性とプライバシーのバランスを取るという課題に直面しています。一部のパーミッションはコア機能に不可欠です (例: カメラアプリはカメラアクセスを必要とします) が、過剰なパーミッションは不要なデータ収集や潜在的なプライバシー侵害につながる可能性があります。

ユーザーの視点から、プライバシーの懸念はパーミッション付与をためらうことにつながり、場合によってはプライバシーとアプリの機能性のいずれかを選ばざるを得なくなり、パーミッション付与を拒否するとアプリが使用できなくなる可能性があります。逆に、ユーザーは影響を十分に理解せずにパーミッションを付与し、意図しないデータ露出につながる可能性があります。

### 事前インストール済みアプリ

Pre-installed apps frequently come with excessive permissions that users cannot control or revoke, as they are often granted by default without explicit consent. This lack of control can result in continuous data collection and persistent privacy risks.

### サードパーティライブラリ (SDK)

**Third-party libraries (SDKs)** further complicate permission management by inheriting app permissions and introducing privacy and security risks that are difficult to audit and control. Mobile permission models often fail to distinguish between permissions granted to an app and those assigned to third-party components, a challenge highlighted in the [IEEE research paper "Engineering Privacy in Smartphone Apps"](https://ieeexplore.ieee.org/document/9001128) (Section IV, _"Third-party content"_). Furthermore, third-party services behind these SDKs may continue accessing data collected over the network even after permissions are revoked or the app is deleted, creating long-term risks for user privacy.

## 流入の形態

- **Requesting Excessive Permissions**: Apps requesting more permissions than necessary for their core functionality.
- **Lack of Use of Privacy-Friendly Alternatives**: Failing to use privacy-friendly alternatives to permissions that are less intrusive and provide users with more control over their data. For example, using coarse location instead of fine location, or using an image picker instead of requesting access to the camera and photo gallery.
- **Lack of Proactive Permission Revocation**: Not automatically revoking app permissions that are no longer necessary, resulting in unnecessary data access over time.
- **Inadequate Permission Explanations**: Failing to provide clear explanations for why each permission is required.

## 影響

- **Violation of User Privacy**: Users may have their personal data unnecessarily accessed by mobile apps, leading to potential misuse, identity theft, or surveillance.
- **Loss of User Trust**: Users may lose trust in an app if it requests unnecessary permissions or does not allow them to revoke permissions that are no longer relevant. This can lead to negative reviews, lower user engagement, and reduced retention.
- **Legal and Compliance Issues**: Apps that improperly manage permissions may face non-compliance with privacy regulations like GDPR or CCPA, which require data minimization and appropriate user control over data access, resulting in potential fines, legal action, or removal from app stores.
- **Malicious Abuse:** Harmful apps can misuse permissions from privileged apps to record, track, or steal data without user consent.
- **Data Breaches:** Once sensitive data leaves the app, its security can no longer be guaranteed, increasing the risk of large-scale data exposure via data breaches.

## 緩和策

- **Enable Proactive Permission Revocation**: Automatically revoke permissions that are no longer necessary to minimize unnecessary data access over time. Ensure that users can manually revoke permissions at any time through a clear and accessible interface.
- **Prefer Privacy-Friendly Alternatives**: Use privacy-friendly alternatives to permissions that are less intrusive and provide users with more control over their data. For example, use coarse location instead of fine location, or use an image picker instead of requesting access to the camera and photo gallery.
- **Limit Permissions to Essential Needs**: Ensure apps only request permissions necessary for core functionality, avoiding the collection of unnecessary data and adhering to the principle of data minimization.
- **Implement Just-in-Time Permission Requests**: Request permissions only when they are needed, providing clear explanations for why each permission is required. This approach helps build user trust and ensures users understand the implications of granting access to their data.
- **User Education on Permissions**: Educate users about why specific permissions are needed and how they can manage these permissions. Providing transparency builds user trust and ensures users understand the importance and relevance of each permission.
