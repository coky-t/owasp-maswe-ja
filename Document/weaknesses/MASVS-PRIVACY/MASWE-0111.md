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

- **Unclear or Absent Privacy Policy**: Not providing a privacy policy, or having one that is not easily accessible or clear to the user, or that doesn't specifically address the data practices of that particular app, instead being a generic document that covers multiple services.
- **Discrepancies in Policy vs Behavior**: Differences between the privacy policy and the app's actual behavior.

## 影響

- **Violation of User Privacy**: Users may unknowingly provide data without understanding how it will be used, exposing them to privacy risks, such as data sharing with third parties, profiling, or targeted advertising without explicit consent.
- **Loss of User Trust**: Users are more likely to lose trust in an app that lacks transparency, which may lead to negative reviews, decreased user engagement, and reduced retention rates.
- **Legal and Compliance Issues**: Failure to provide an adequate privacy policy can result in non-compliance with privacy laws and regulations, such as GDPR or CCPA, potentially leading to fines, legal action, or removal from app stores.

## 緩和策

- **Provide a Clear Privacy Policy**: Make sure a comprehensive and understandable privacy policy is readily accessible to users. Tailor it to the specific data practices of your app and write it in clear, understandable language as stated in Article 12 of the GDPR.
- **Ensure Consistency in Privacy vs Behavior**: Keep your data collection practices documented and up to date in privacy policies, privacy labels, and app store listings. Ensure that these documents match the app's actual behavior to avoid discrepancies that could mislead users or violate platform policies.
- **Regularly Review and Update Privacy Policy**: Regularly review and update the privacy policy to reflect any changes in data collection practices, new features, or modifications to existing features that may impact how user data is handled.
