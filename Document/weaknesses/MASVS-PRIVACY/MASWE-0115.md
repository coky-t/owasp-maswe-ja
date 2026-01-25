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

- **ユーザープライバシーの侵害**: 曖昧な同意メカニズムが使用されると、ユーザーが知らないうちに自身のデータに対するコントロールを放棄してしまう可能性があり、ユーザープライバシーがひどく侵害されます。これは、明確な同意や十分な情報に基づく同意なしに、ユーザーが不快または有害と感じる目的 (ターゲット広告、プロファイリング、差別、さらにはアイデンティティ窃取など) に情報が使用されるリスクにさらします。
- **ユーザーの信頼の喪失**: ユーザーはアプリへの信頼を失い、アプリを放棄したり、否定的なレビューを共有したり、他のユーザーにアプリの使用を思いとどまられる可能性があり、評判を損ない、ビジネスの損失につながる可能性があります。
- **法的およびコンプライアンスの問題**: 法律やプラットフォームの要件を遵守しないと、法的措置、罰金、アプリストアからの削除につながる可能性があります。

## 緩和策

- **変更時に同意を促す**: データ収集方法に変更がある場合や、追加データが収集される場合に、ユーザーに同意を促すメカニズムを確立し、アプリ機能が進化する際の透明性を確保します。
- **即時アクションについて明確で明示的なユーザー同意を取得する**: センサやローカルデータ (カメラ、位置情報など) などの機密性の高いリソースにアクセスする前に、常にユーザーから明示的な許可を要求します。iOS では [目的の文字列](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources)、Android では [同様のプロンプト](https://developer.android.com/training/permissions/requesting#explain) などのメカニズムを使用して、許可が必要とされる理由を明確に説明し、ユーザーが自分のデータの即時使用を理解するようにします。
- **情報に基づいた透明性のある同意を確保する**: 収集されるデータの種類、その使用方法、潜在的な影響について、明確かつ具体的な情報をユーザーに提供します。同意は、サービス規約に隠されたり、将来の使用にまとめたりしてはいけません。特に最初の要求を超えて許可を拡張する場合、ユーザーは目的ごとに個別に同意を確認しなければなりません。
