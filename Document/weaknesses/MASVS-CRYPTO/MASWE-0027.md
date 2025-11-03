---
title: 不適切な乱数生成 (Improper Random Number Generation)
id: MASWE-0027
alias: improper-random-number-generation
platform: ["android", "ios"]
profiles: ["L1", "L2"]
mappings:
  masvs-v1: [MSTG-CRYPTO-6]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [332, 337, 338]
  android-risks: 
  - https://developer.android.com/privacy-and-security/risks/weak-prng
observed_examples:
- https://nvd.nist.gov/vuln/detail/CVE-2013-6386
- https://nvd.nist.gov/vuln/detail/CVE-2013-6386
- https://nvd.nist.gov/vuln/detail/CVE-2006-3419
- https://nvd.nist.gov/vuln/detail/CVE-2008-4102
- https://www.zellic.io/blog/proton-dart-flutter-csprng-prng/
status: new
---

## 概要

[擬似乱数生成器 (PRNG)](https://en.wikipedia.org/wiki/Pseudorandom_number_generator) アルゴリズムは、予測可能なエントロピーが不十分なシードに基づいてシーケンスを生成します。一般的な実装は暗号論的に安全ではありません。たとえば、一般的に線形合同法を使用するため、十分な観測出力があれば、攻撃者が将来の出力を予測できます。したがって、セキュリティが重要なアプリケーションや機密データの保護には適していません。

## 影響

- **保護メカニズムのバイパス**: 認証などのセキュリティコンテキストで、暗号論的に安全でない PRNG を使用すると、重大なリスクを引き起こします。攻撃者は生成された数値を推測し、特権データや機能にアクセスできる可能性があります。乱数を予測または再生成すると、暗号の侵害、機密性の高いユーザー情報の漏洩、ユーザーのなりすましにつながる可能性があります。

## 流入の形態

- **リスクのあるランダム API**: アプリは多くの既存 API を使用し、不十分なエントロピーの乱数を生成します。
- **非ランダムソース**: アプリは、現在の時刻などの非ランダムソースを使用して、「ランダムと考えられる」値を作成するカスタムメソッドを使用する可能性があります。

## 緩和策

セキュリティ関連のコンテキストでは、暗号論的に安全な乱数を使用します。

一般的に、たとえ安全なものであっても、特にハードコードされたシード値 (逆コンパイルによってさらされる脆弱となる) を含む、ランダム関数を決定論的な方法で使用しないことを強く推奨します。

乱数生成に関する詳細情報と推奨事項については [RFC 1750 - Randomness Recommendations for Security](https://www.ietf.org/rfc/rfc1750.txt) および [OWASP Cryptographic Storage Cheat Sheet - Secure Random Number Generation](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html#secure-random-number-generation) を参照してください。
