---
title: リスクのある暗号実装 (Risky Cryptography Implementations)
id: MASWE-0019
alias: potentially-weak-crypto-impl
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2]
  masvs-v2: [MASVS-CRYPTO-1, MASVS-CODE-3]
  mastg-v1: [MASTG-TEST-0061, MASTG-TEST-0014]
  cwe: [326, 327, 1240]

refs: 
 - https://book.hacktricks.xyz/crypto-and-stego/cryptographic-algorithms
 - https://eudl.eu/pdf/10.4108/eai.3-12-2015.2262471
 - https://www.scitepress.org/papers/2014/50563/50563.pdf
 - https://pure.tugraz.at/ws/portalfiles/portal/23858147/main.pdf
 - https://github.com/Wind-River/crypto-detector
 - https://github.com/Rami114/cryptoscan/
 - https://github.com/IAIK/CryptoSlice
 - https://developer.android.com/reference/javax/crypto/Cipher#getInstance(java.lang.String)
 - https://developer.android.com/privacy-and-security/security-gms-provider
 - https://developer.android.com/privacy-and-security/cryptography#bc-algorithms
 - https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library
 - https://developer.android.com/privacy-and-security/cryptography#crypto_provider
 - https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
 - https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile
---

## 概要

リスクのある暗号実装、または、FIPS 140-2/3 (Federal Information Processing Standards) などの確立されたセキュリティ標準を満たしていないものなどの非準拠の暗号実装は、十分にテストされていないアルゴリズムや認定を受けていないアルゴリズムを使用する可能性があり、安全な鍵管理のベストプラクティスに従っていない可能性があり、厳密なピアレビューや形式検証を受けていないカスタム暗号ソリューションを含む可能性があります。

## 影響

確立された標準に従わずに作成されたカスタム暗号実装はブルートフォースや差分暗号解析などの攻撃の影響を受けやすくなります。さらに、暗号を正しく実装することは非常に困難であり、正しくないパディングや欠陥のある乱数生成といった、カスタムソリューションの小さなエラーでさえ、システムのセキュリティを完全に弱体化する可能性があり、攻撃者に機密データをさらす可能性があります。

そのような欠陥に伴う影響は非常に広範に及ぶ可能性があり、予測や測定が困難になります。

- **データ侵害**: リスクのある暗号実装は機密データの不正アクセスにつながり、データ侵害をもたらす可能性があります。
- **機密性、完全性、真正性の侵害**: 暗号の主要な原則 (機密性、完全性、真正性) が侵害されます。攻撃者は、正当なユーザーやシステムを復号、操作、なりすますことが可能です。

## 流入の形態

- **標準ライブラリからの逸脱**: Conscrypt や CryptoKit などのプラットフォームによって提供されるライブラリや、OpenSSL、BouncyCastle などの他の十分に確立されたライブラリを使用していません。
- **暗号定数の使用**: ハードコードされた暗号定数は一般的に暗号アルゴリズムの実装に使用されます。これらの定数には、ブロック暗号の S ボックス (置換ボックス)、順列表などがあります。
- **低レベル算術演算の使用**: 暗号アルゴリズムで一般的に使用される低レベル算術演算 (ビット演算、シフト、カスタムパディングスキームなど)。
- **高エントロピーコード**: 暗号実装または、暗号アルゴリズムをリバースエンジニアリングから隠す可能性のある高度に難読化されたコードの指標。
- **非暗号関数の使用**: 暗号化の代わりの Base64 エンコーディングや XOR などの非暗号関数。

## 緩和策

- **標準の暗号ライブラリを使用し、カスタム暗号を避ける**: カスタム暗号アルゴリズムやプロトコルの開発は避けます。OpenSSL、BoringSSL などの十分に確立されて広く受け入れられている暗号ライブラリ、または Android の Conscrypt や Apple の CryptoKit などのプラットフォーム固有のライブラリを常に優先します。これらのライブラリは広範のテストを受け、新たなセキュリティ脅威に対処するために定期的に更新されています。

- **セキュリティ標準への準拠を確認する**: カスタム暗号の使用を避けられない場合は、FIPS 140-2/3 (Federal Information Processing Standards) や最新の National Institute of Standards and Technology (NIST) の推奨事項などの業界標準を満たすように実装されていることを確認します。
- **定期的にセキュリティ監査を実施する**: カスタム暗号の使用が避けられない場合は、定期的なセキュリティ監査 (徹底的なコードレビューを含む) を実施し、カスタム暗号実装の欠陥を特定して修復します。外部のセキュリティ専門家に依頼し、公平な評価を受けます。
