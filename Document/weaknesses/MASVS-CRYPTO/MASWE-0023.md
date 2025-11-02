---
title: リスクのあるパディング (Risky Padding)
id: MASWE-0023
alias: risky-padding
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CRYPTO-1]
  mastg-v1: [MASTG-TEST-0014]
  cwe: [208, 325, 327, 780]

refs:
- https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile
- https://www.usenix.org/legacy/event/woot10/tech/full_papers/Rizzo.pdf
- https://capec.mitre.org/data/definitions/463.html
- https://robertheaton.com/2013/07/29/padding-oracle-attack/
- https://cryptopals.com/sets/3/challenges/17
- https://medium.com/@masjadaan/oracle-padding-attack-a61369993c86
status: new
---

## 概要

[パディングオラクル攻撃](https://www.usenix.org/legacy/event/woot10/tech/full_papers/Rizzo.pdf) はサイドチャネルエクスプロイトの一種であり、攻撃者が鍵を知ること **なしで** データを復号または操作できます。これらの攻撃はパディングスキーム自体が破綻することによるものではなく、アプリがパディングエラーが発生したかどうかを (エラーメッセージやタイミングのずれを通じて) 明らかにし、**オラクル** を作成することで発生します。改変された暗号文を送信し、アプリのレスポンスを観察することで、攻撃者は段階的に平文を復元したり、暗号文を偽造でき、機密性と完全性の両方を侵害します。

以下は、リスクのあるパティングが問題になる可能性がある、暗号コンテキストの二つの一般的な例です。

- **対称暗号**: ブロック暗号モード (AES-CBC など) では、**PKCS#7 パティング** が広く使用されており、破られてはいません (NIST によって禁止されていません)。しかし、システムが詳細なエラーメッセージやタイミングのずれを漏洩した場合、パティングオラクル攻撃に対して脆弱になります。これを緩和するには、暗号学者は AES-GCM などの **認証付き暗号モード** を使用するか、AES-CBC を別の完全性チェック (Encrypt-then-MAC スキームの HMAC など) とペアにすることがよくあります。
- **非対称暗号**: RSA では、**PKCS#1 v1.5** は [Bleichenbacher](https://link.springer.com/content/pdf/10.1007/BFb0055716.pdf) のような (パティングオラクルに基づく) 攻撃 の影響を受けやすいことが知られています。この古いスキームは現在さまざまな標準 (たとえば、2016 年 11 月の [RFC 8017, Section 7.2](https://datatracker.ietf.org/doc/html/rfc8017#section-7.2) や 2019 年 3 月の [NIST SP 800-131A Rev.2, Section 6](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf) を参照) で非推奨または禁止されています。

しかし、パティングオラクル攻撃を受けやすいパディングスキームを使用するだけでは、脆弱性を保証していません。上述のように、アプリは、パディングエラーが発生したかどうかを示す情報 (「オラクル」) を漏洩すること **も** 必要です。両方の条件が満たされる場合、攻撃者はこれらのシグナルを使用して機密データを復元したり、悪意のある暗号文を作成できます。

## 影響

- **Loss of Integrity**: Attackers can modify ciphertext, exploiting the padding oracle to trick the system into accepting maliciously altered data, leading to unauthorized data modifications.
- **Loss of Confidentiality**: Attackers can use the padding oracle to iteratively decrypt sensitive information, such as passwords or session tokens, leading to exposure of confidential data.

## 流入の形態

- **Unauthenticated Padding for Symmetric Encryption**: Using padding schemes like PKCS#7 without authenticating the ciphertext (e.g., with HMAC) allows padding oracle attacks in modes like AES-CBC.
- **Risky Padding in Asymmetric Encryption**: Using schemes like PKCS#1 v1.5 for RSA encryption without strict, uniform handling of invalid ciphertext enables oracle attacks.
- **Exposure of Cryptographic Errors**: Revealing detailed error messages or timing variations during decryption can leak information exploitable by attackers.

## 緩和策

- **Use Authenticated Symmetric Encryption Modes**: Prefer authenticated encryption modes like AES-GCM, which eliminate the need for separate padding validation and incorporate integrity checks. If AES-CBC must be used, adopt the Encrypt-then-MAC paradigm (e.g., append HMAC). See [NIST SP 800-175B Rev.1, Section 4.3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf).
- **Use Secure Padding Schemes for Asymmetric Encryption**: Replace risky schemes like PKCS#1 v1.5 with secure ones such as OAEP (Optimal Asymmetric Encryption Padding). See [NIST SP 800-56B Rev.2, Section 7.2.2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-56Br2.pdf).
- **Don't Expose Cryptographic Errors**: Do not expose cryptographic error messages, such as padding errors, to users. This prevents attackers from gaining clues about the padding's correctness.
