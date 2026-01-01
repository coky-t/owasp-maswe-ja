---
title: 不十分なデータ収集宣言 (Inadequate Data Collection Declarations)
id: MASWE-0112
alias: data-collection-declarations
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: [MSTG-STORAGE-12]
  masvs-v2: [MASVS-PRIVACY-3]
  cwe: [359]
refs:
- https://support.apple.com/en-us/102188
- https://support.apple.com/kb/HT211970
- https://developer.apple.com/app-store/review/guidelines/#5.1.2
- https://developer.apple.com/app-store/app-privacy-details/#data-collection
- https://support.google.com/googleplay/android-developer/answer/10787469
- https://developer.apple.com/videos/play/wwdc2023/10060
- https://support.google.com/googleplay/answer/11416267
- https://www.youtube.com/watch?v=J7TM0Yy0aTQ
- https://www.youtube.com/watch?v=4rfF3y4xchU
status: new
---

## 概要

Apple の [App Privacy Report](https://support.apple.com/en-us/102188) や [Privacy Nutrition Labels](https://support.apple.com/kb/HT211970)、または Google の [Data Safety section](https://support.google.com/googleplay/android-developer/answer/10787469?hl=en) に記載されているようなモバイルアプリの明言されたデータ収集方法が不完全であったり、アプリの実際の動作と一致しない場合、ユーザーは、データが自分のアイデンティティにリンクされているか、追跡に使用されているか、サードパーティと共有されているかどうかを理解することなど、自分のプライバシーについて十分な情報に基づいた判断を下すことができません。

これらの宣言では、収集されるデータ、その使用方法、ユーザーのアイデンティティにリンクされるかどうか、プラットフォームのポリシーに従ってサードパーティと共有されるかどうかを明確に示す必要があります。

**サードパーティライブラリ (SDK) に関する注意**: 開発者は、データ管理者として、[ENISA による GDPR コンプライアンスに関する調査](https://www.enisa.europa.eu/sites/default/files/publications/WP2017%20O-2-2-4%20GDPR%20Mobile.pdf) (Section 2.2.7, _"Data transfers and processing by third parties"_) でハイライトされているように、サードパーティコンポーネントが機密データを合法的で、公平で、透明性のある処理をすることを確保する法的責任を負います。但し、場合によっては、モバイルアプリ開発者がこれらのサードパーティ SDK が実際にどのようにデータを収集しているかを完全に把握することが困難なことがあります。

## 流入の形態

- **宣言されていないデータ収集と目的**: 収集されるデータの内容 (位置情報、連絡先、識別子など) とその目的 (分析、パーソナライゼーションなど) を宣言しておらず、ユーザーは自分の情報がどのように使用されるかわからないままです。
- **宣言と動作の不一致**: プライバシーラベル宣言 (Apple の Privacy Nutrition Labels や Google の Data Safety Section など) とアプリの実際の動作との相違 (宣言されていないデータ収集、プライバシーラベルに記載されていないサードパーティとの共有、開示されていない目的でのデータ使用など) は、Apple と Google の両方のガイドラインに反しています。

## 影響

- **Violation of User Privacy**: Users may unknowingly share data without fully understanding its purpose, which can lead to unauthorized sharing, profiling, or targeted advertising.
- **Loss of User Trust**: Inconsistent declarations can result in users losing trust in the app, leading to negative reviews, lower user engagement, and reduced retention.
- **Legal and Compliance Issues**: Inaccurate or inconsistent data declarations may lead to non-compliance with regulations like GDPR or CCPA, resulting in potential fines, legal action, or removal from app stores.

## 緩和策

- **Maintain Accurate Privacy Labels**: Comply with Apple's Privacy Nutrition Labels and Google's Data Safety Section requirements by providing accurate and transparent information about your data practices, including data collection and sharing with third parties.
- **Ensure Consistency in Declarations vs Behavior**: Keep your data collection practices documented and up to date in privacy policies, privacy labels, and app store listings. Ensure that these documents match the app's actual behavior to avoid discrepancies that could mislead users or violate platform policies.
