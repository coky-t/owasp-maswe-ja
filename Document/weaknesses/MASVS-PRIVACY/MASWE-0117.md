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

事前インストール済みアプリは、ユーザーが制御または取り消しできない過剰なパーミッションを付与していることがよくあります。多くの場合、それらは明示的な同意なしにデフォルトで付与されているためです。この制御の欠如は継続的なデータ収集や永続的なプライバシーリスクにつながる可能性があります。

### サードパーティライブラリ (SDK)

**サードパーティライブラリ (SDK)** はアプリのパーミッションを継承することでパーミッション管理をさらに複雑化し、監査や対策が困難なプライバシーとセキュリティのリスクをもたらします。モバイルのパーミッションモデルは、アプリに付与されたパーミッションとサードパーティコンポーネントに割り当てられたものの間で区別できないことが多く、この課題は [IEEE 研究論文 "Engineering Privacy in Smartphone Apps"](https://ieeexplore.ieee.org/document/9001128) (Section IV, _"Third-party content"_) で強調されています。さらに、これらの SDK の背後にあるサードパーティサービスは、パーミッションが取り消された後やアプリが削除された後でも、ネットワーク経由で収集されたデータにアクセスし続ける可能性があり、ユーザーのプライバシーに対して長期的なリスクをもたらします。

## 流入の形態

- **過剰なパーミッションの要求**: アプリはコア機能に必要よりも多くのパーミッションを要求します。
- **プライバシーに配慮した代替手段の使用の欠如**: ユーザーを邪魔せず、データに対するより多くのコントロールを提供する、プライバシーに配慮した代替手段をパーミッションに使用していません。たとえば、詳細な位置情報ではなく大まかな位置情報を使用したり、カメラやフォトギャラリーへのアクセスを要求する代わりに画像ピッカーを使用します。
- **積極的なパーミッション失効の欠如**: もはや必要ではないアプリのパーミッションを自動的に取り消さず、時間の経過とともに不要なデータアクセスにつながります。
- **不適当なパーミッションの説明**: 各パーミッションが必要な理由について明確な説明を提供していません。

## 影響

- **ユーザープライバシーの侵害**: ユーザーが持つ個人データをモバイルアプリにより不必要にアクセスされ、不正使用、アイデンティティ窃取、偵察につながる可能性があります。
- **ユーザーの信頼の喪失**: アプリが不要なパーミッションを要求したり、もはや関係のないパーミッションを取り消せない場合、ユーザーはアプリの信頼を失う可能性があります。これは、否定的なレビュー、ユーザーエンゲージメントの低下、リテンションの低下につながる可能性があります。
- **法的およびコンプライアンスの問題**: パーミッションを適切に管理していないアプリは、GDPR や CCPA などのプライバシー規制の非遵守に直面する可能性があります。これらはデータ最小化と、データアクセスに対する適切なユーザー制御を要求しており、罰金、法的措置、アプリストアからの削除につながる可能性があります。
- **悪意のある不正使用:** 有害なアプリは、特権アプリのパーミッションを悪用して、ユーザーの同意なしにデータを記録、追跡、窃取する可能性があります。
- **データ侵害:** 機密データがアプリから離れると、そのセキュリティは保証されなくなり、データ侵害による大規模なデータ開示のリスクが高まります。

## 緩和策

- **Enable Proactive Permission Revocation**: Automatically revoke permissions that are no longer necessary to minimize unnecessary data access over time. Ensure that users can manually revoke permissions at any time through a clear and accessible interface.
- **Prefer Privacy-Friendly Alternatives**: Use privacy-friendly alternatives to permissions that are less intrusive and provide users with more control over their data. For example, use coarse location instead of fine location, or use an image picker instead of requesting access to the camera and photo gallery.
- **Limit Permissions to Essential Needs**: Ensure apps only request permissions necessary for core functionality, avoiding the collection of unnecessary data and adhering to the principle of data minimization.
- **Implement Just-in-Time Permission Requests**: Request permissions only when they are needed, providing clear explanations for why each permission is required. This approach helps build user trust and ensures users understand the implications of granting access to their data.
- **User Education on Permissions**: Educate users about why specific permissions are needed and how they can manage these permissions. Providing transparency builds user trust and ensures users understand the importance and relevance of each permission.
