---
title: 不十分なプライバシーポリシー (Inadequate Privacy Policy)
id: MASWE-0111
alias: privacy-policy
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: [MASVS-STORAGE-12]
  masvs-v2: [MASVS-PRIVACY-3]
  cwe: [359]
refs:
- https://support.google.com/googleplay/android-developer/answer/9859455#privacy_policy
- https://developer.apple.com/app-store/app-privacy-details/#privacy-links
- https://developer.apple.com/app-store/review/guidelines/#5.1.1
status: new
---

## 概要

モバイルアプリは、ユーザーデータがどのように収集、処理、共有、保護されるかについて、明確かつ包括的な説明をユーザーに提供しなければなりません。プライバシーポリシーは、容易にアクセスでき、当該のアプリにあわせて調整され、ユーザーが理解しやすい方法で記述されている必要があります。堅牢なプライバシーポリシーなしでは、ユーザーは自身のデータについて十分な情報に基づいた判断を下すことができず、自身の情報がどのように使用や共有されているかを認識できない可能性があります。

不完全、曖昧、あるいはアプリの動作と一致しないプライバシーポリシーはユーザーに誤解を招き、透明性の欠如につながり、プライバシー侵害や開発者に対する法的影響につながる可能性があります。

## 流入の形態

- **不明確または存在しないプライバシーポリシー**: プライバシーポリシーを提供していない、ユーザーが容易にアクセスできない、明確ではない、または、特定のアプリのデータ処理方法について具体的に言及しておらず、複数のサービスをカバーする一般的な文書となっています。
- **ポリシーと動作の不一致**: プライバシーポリシーとアプリの実際の動作に相違があります。

## 影響

- **ユーザープライバシーの侵害**: ユーザーはデータが使用される方法を理解せずに無意識のうちにデータを提供してしまい、サードパーティとのデータ共有、プロファイリング、明示的な同意なしでのターゲット広告など、プライバシーリスクにさらす可能性があります。
- **ユーザーからの信頼の喪失**: ユーザーは透明性を欠如したアプリの信頼を失いやすく、否定的なレビュー、ユーザーエンゲージメントの下落、リテンション率の低下につながる可能性があります。
- **法的およびコンプライアンスの問題**: 適切なプライバシーポリシーを提供しないと、GDPR や CCPA などのプライバシー法規制に非準拠となる可能性があり、罰金、法的措置、アプリストアからの削除につながる可能性があります。

## 緩和策

- **Provide a Clear Privacy Policy**: Make sure a comprehensive and understandable privacy policy is readily accessible to users. Tailor it to the specific data practices of your app and write it in clear, understandable language as stated in Article 12 of the GDPR.
- **Ensure Consistency in Privacy vs Behavior**: Keep your data collection practices documented and up to date in privacy policies, privacy labels, and app store listings. Ensure that these documents match the app's actual behavior to avoid discrepancies that could mislead users or violate platform policies.
- **Regularly Review and Update Privacy Policy**: Regularly review and update the privacy policy to reflect any changes in data collection practices, new features, or modifications to existing features that may impact how user data is handled.
