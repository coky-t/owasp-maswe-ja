---
title: 匿名化対策や仮名化対策の欠如 (Lack of Anonymization or Pseudonymisation Measures)
id: MASWE-0109
alias: anonymization-pseudonymization-measures
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-2]
  cwe: [359]
refs:
- https://cloud.google.com/sensitive-data-protection/docs/classification-redaction
- https://gdpr-info.eu/recitals/no-26/
- https://gdpr-info.eu/recitals/no-28/
- https://gdpr-info.eu/art-4-gdpr/
- https://ec.europa.eu/justice/article-29/documentation/opinion-recommendation/files/2014/wp216_en.pdf
- https://www.statista.com/topics/9460/app-tracking-and-mobile-privacy/
status: new
---

## 概要

データ抽象化、匿名化、仮名化などの連結不可能性技法がなければ、異なるサービス間や長期にわたってユーザーの識別と追跡を可能にできます。匿名化は、ランダム化や汎化などの手法を通じて、位置情報の難読化や機密属性のスクランブル化など、データの削除または変更することで個人を不可逆的に匿名化します。対照的に、仮名化は識別可能なデータをトークンまたはハッシュ地に置き換えることで、より安全になりますが、一定の条件下では技術的に元に戻すことも可能です。

このようなプライバシー保護の欠如は、不正なプロファイリング、同意のないターゲッティング広告、プライバシー規制違反による潜在的な法的責任につながる可能性があります。

## 流入の形態

- **匿名化対策や仮名化対策の欠如**: サーバーサイドの収集前にユーザー ID や名前などの直接的な識別子をデータから削除していない、または実世界のアイデンティティとの関連付けを防ぐためにデータを操作していない。これにはプライバシーを強化するための Private Information Retrieval や Oblivious HTTP (OHTTP) などのプロトコルを実装していないことも含みます。

## 影響

- **ユーザープライバシーの侵害**: ユーザーは自分の個人情報が追跡目的で収集されていることに気付かず、プライバシー侵害につながる可能性があります。
- **コンプライアンスおよび法的リスク**: データ保護の法律や規制 (GDPR など) の違反は法的措置や罰金につながります。

## 緩和策

- **Use Anonymisation and Pseudonymisation**: Ensure techniques like anonymisation and pseudonymisation are implemented to prevent user identification.
