---
title: 不適切な暗号鍵生成 (Improper Cryptographic Key Generation)
id: MASWE-0009
alias: weak-crypto-key-generation
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2]
  masvs-v2: [MASVS-CRYPTO-2]
  cwe: [331, 337, 338]
  android-risks: 
    - https://developer.android.com/privacy-and-security/risks/weak-prng
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://developer.android.com/privacy-and-security/cryptography
- https://developer.android.com/reference/javax/crypto/KeyGenerator

status: new
---

## 概要

暗号において、セキュリティの強度は暗号鍵を生成するために使用される手法に大きく影響を受けます。重要な側面の一つは鍵サイズ (鍵長とも呼ばれます) であり、ビット単位で測定され、最新のセキュリティベストプラクティスに準拠する必要があります。不十分な鍵サイズを使用する暗号アルゴリズムは攻撃に脆弱であり、鍵が長いほど一般的により複雑な暗号になります。

しかし、鍵サイズが十分に大きくても、鍵生成プロセスに欠陥があれば暗号のセキュリティが侵害される可能性があります。十分なエントロピーを持つ強力で暗号論的にセキュアな擬似乱数生成器 (CSPRNG) を使用しないと、攻撃者が推測したり再現しやすく、繰り返しパターンの影響を受けやすい、予測可能な鍵を生成する可能性があります。

## 影響

- **ブルートフォース攻撃のリスク**: 短い鍵長や予測可能な乱数生成器 (PRNG) の入力値による、不適切な鍵生成はブルートフォース攻撃のリスクが高まります。攻撃者は容易に鍵を推測したり、正しい鍵を見つけるまで可能な鍵を体系的に試すことができます。
- **機密性の喪失**: 暗号化は、機密データの機密性を維持するために、強力な鍵に依存しています。エントロピーが不十分なシード値は、攻撃者が機密情報を復号してアクセスでき、不正な開示や潜在的なデータ侵害につながる可能性があります。
- **完全性の喪失**: 不適切な鍵生成はデータの完全性を損ない、攻撃者が脆弱性を悪用して、検出されずに情報を改変や改竄する可能性があります。

## 流入の形態

- **不十分なエントロピー**: 不十分なエントロピーのランダム性のソースを使用すると、予測可能な暗号鍵につながる可能性があります。
- **不十分な鍵長**: 短すぎる暗号鍵は不適当なセキュリティを提供します。たとえば、細心のアルゴリズムで推奨される長さより短い鍵はブルートフォース攻撃に脆弱となり、攻撃者が簡単に解読できる可能性があります。
- **リスクのあるアルゴリズムや破られたアルゴリズムの使用**: 非推奨であったり、リスクがあったり、本質的に破られている暗号アルゴリズムはより弱い鍵の生成につながる可能性があります。これらのアルゴリズムは脆弱性を抱えていたり、短い鍵長しかサポートしていないため、最新の攻撃に影響を受けやすくなり、アプリ全体のセキュリティを損なうことがよくあります。

## 緩和策

- エントロピー生成と鍵管理のベストプラクティスに従う、最新の、十分に確立された暗号ライブラリと API を常に使用します。
- 鍵長が、AES 暗号の場合は 256 ビット、RSA (量子コンピューティング攻撃を考慮) の場合 2048 ビットなど、暗号セキュリティの現在の標準を満たすか超えていることを確認してください。暗号鍵サイズの詳細情報については ["NIST Special Publication 800-57: Recommendation for Key Management: Part 1 – General"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf)、["NIST Special Publication 800-131A: Transitioning the Use of Cryptographic Algorithms and Key Lengths"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf)、["BlueKrypt's Cryptographic Key Length Recommendation"](https://www.keylength.com/) を参照してください。
