---
title: 不十分または曖昧なユーザー同意メカニズム (Inadequate or Ambiguous User Consent Mechanisms)
id: MASWE-0115
alias: ambiguous-consent-mechanisms
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-4]
  cwe: [359]
refs:
- https://developer.apple.com/design/human-interface-guidelines/privacy#Requesting-permission
- https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources
- https://developer.android.com/training/permissions/requesting#explain
status: new
---

## 概要

[EU の GDPR](https://gdpr-info.eu/art-7-gdpr/), [カリフォルニアの CCPA](https://cppa.ca.gov/regulations/pdf/cppa_act.pdf), [ブラジルの LGPD](https://lgpd-brazil.info/chapter_02/article_08), [カナダの PIPEDA](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/p_principle/principles/p_consent/) などのさまざまな国際プライバシー規制に従い、データ処理の前に、ユーザーの同意を明示的かつ十分な情報に基づいて取得する必要があります。ユーザーは、データ収集の目的と、同意を与えた場合の潜在的な結果を十分に認識する必要があります。さらに、同意は、処理されるデータに固有の能動的な選択である必要があり、他のサービス契約とバンドルされたり、曖昧または強制的な方法で提示されてはいけません。

これらの原則に従わないモバイルアプリは、ユーザーが知らないうちにデータの収集や処理に同意してしまう結果となり、基本的な権利や自由に重大なリスクをもたらす可能性があります。たとえば、アプリは曖昧または交渉の余地のない同意を求め、ユーザーがその意味を十分に理解しないまま同意を迫ることがあります。

さらに、ユーザーはいつでも簡単に同意を撤回でき、アプリの機能への潜在的な影響を含め、その方法を明確に通知する必要があります。開発者は、ユーザーの同意の記録を保持し、同意の要求が明確で、他の条件とは区別され、法的に有効であることを確保し、データ処理の全範囲を不明瞭にするような慣行を避けなければなりません。

## 流入の形態

- **同意変更のためのプロンプトの不備**: データ収集方法に変更がある場合や、当初の規定を超えて追加データが収集される場合に、ユーザーに同意を求めていません。
- **曖昧な同意メカニズム**: 同意は利用規約にバンドルされており、多くの場合、ユーザーに再度通史することなく、将来のユースケースをカバーしています。場合によっては、ユーザーが明示的にアクセスを拒否しない限り、同意が暗黙的に与えられ、明確な承認なしでのデータ収集につながります。

## 影響

- **Violation of User Privacy**: When ambiguous consent mechanisms are used, user privacy is severely compromised as users may unknowingly give up control over their data. This exposes them to the risk of their information being used without clear or informed consent for purposes they may find objectionable or harmful, such as targeted advertising, profiling, discrimination or even identity theft.
- **Loss of User Trust**: Users may lose trust in the app and abandon it, share negative reviews, or discourage others from using it, leading to reputational damage and potential loss of business.
- **Legal and Compliance Issues**: Non-compliance with laws and platform requirements can result in legal consequences, fines, or removal from app stores.

## 緩和策

- **Prompt for Consent on Changes**: Establish mechanisms for prompting users for consent if data collection practices change or if additional data is being collected, ensuring transparency when app functionality evolves.
- **Obtain Clear and Explicit User Consent for Immediate Actions**: Before accessing sensitive resources like sensors or local data (e.g., camera, location), always request explicit permission from the user. Clearly explain why the permission is needed, using mechanisms like [purpose strings](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources) on iOS or [similar prompts](https://developer.android.com/training/permissions/requesting#explain) on Android, to ensure users understand the immediate use of their data.
- **Ensure Informed and Transparent Consent**: Provide users with clear, specific information about what data will be collected, how it will be used, and the potential impact. Consent should not be hidden in terms of service or bundled for future uses. Users must confirm consent separately for each purpose, especially when permissions extend beyond the initial request.
