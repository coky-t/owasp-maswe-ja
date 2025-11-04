---
title: アプリパッケージにハードコードされた API キー (API Keys Hardcoded in the App Package)
id: MASWE-0005
alias: api-keys-hardcoded-app-package
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-AUTH-1]
  mastg-v1: []
  cwe: [798]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/insecure-api-usage
status: new
refs:
- https://cloud.google.com/docs/authentication/api-keys#securing
- https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions
---

## 概要

アプリパッケージ、ソースコード、またはコンパイルされたバイナリにハードコードされた API キーは、リバースエンジニアリングによって簡単に抽出できます。

## 影響

アプリに API キーをハードコードすると、さまざまなセキュリティ問題につながる可能性があります。以下がありますが、それらに制限されません。

- **金銭的損失**: 攻撃者は、ハードコードされた API キーを侵害して悪用し、不正な API 呼び出しを行い、使用量に応じて課金されるサービス (AI または ML API サービスなど) を不正使用し、アプリ所有者に予期せぬ請求をもたらす可能性があります。
- **システム完全性とビジネス業務の侵害**: 抽出された API キーは、攻撃者に機密性の高いリソースやサービスへの不正アクセスを与える可能性があります。これは、アプリの完全性、プライバシー、サービスの継続性を侵害することで、開発者や企業に直接的な影響を与え、サービス拒否 (DoS) やポリシー違反によるサービス停止などの混乱につながる可能性があります。このようなインシデントはユーザーエクスペリエンスに重大な影響を及ぼし、ユーザーの信頼を失墜し、ビジネスの評判や業務に悪影響を及ぼす可能性があります。
- **保護メカニズムのバイパス**: ハードコードされた API キーはアプリの保護メカニズムのバイパスを容易にする可能性があります。攻撃者はこれを使用して、制限されたコンテンツにアクセスしたり、アプリ機能に不正操作したり、有料を意図した機能をロック解除でき、収益とユーザーエクスペリエンスの両方に影響を及ぼします。

## 流入の形態

API キーは以下の複数の領域にハードコードできます。

- **アプリのソースコード**: アプリのソースコードに直接埋め込まれます。
- **アプリのアセット**: 設定ファイル、マニフェストファイル、リソースファイルなど、最終的に配布するアプリパッケージ (一般的に APK/IPA) に同梱されるファイルに含まれます。
- **ライブラリ**: サードパーティ、ファーストパーティのライブラリやその他のアプリ依存関係の構成ファイルやソースコード。

## 緩和策

- Use a stateful API service that provides secure authentication, client validation, and session controls. Implement dynamic tokens that expire after a reasonably short time (e.g., 1 hour). This can help reduce the impact of key exposure. Also, ensure proper error handling and logging to detect and respond to unauthorized access attempts. Consider using OAuth 2.0 and security libraries like AppAuth to simplify secure OAuth flows.
- If a stateful API service is not viable, consider using a stateless API service with a middleware solution (sometimes known as API proxy or API Gateway). This involves proxying requests between the app and API endpoint. Use JSON Web Tokens (JWT) and JSON Web Signature (JWS) to store the vulnerable static key server-side rather than in the application (client). Implement secure key management practices and consider using a cloud key management service.
- If API keys must be hardcoded, be sure to configure them with the minimum required permissions to reduce the impact in case of exposure. Many services allow you to create keys with restricted access, which limits the operations that can be performed.
- Consider using a [Key Management Service](https://cloud.google.com/kms/docs/key-management-service) to get API keys on runtime after validating app integrity.
- Regularly audit the codebase and dependencies for hardcoded sensitive data (e.g. using tools such as [gitLeaks](https://github.com/gitleaks/gitleaks)).
- Use white-box cryptography techniques to encrypt API keys and sensitive data within the app, ensuring that the cryptographic algorithms and keys remain protected even if the app is reverse-engineered.
- While not foolproof, and **to be used as a last resort** when no other secure options are available, code and resource obfuscation and encryption can deter attackers by making it more difficult to analyze your app and discover hardcoded secrets. Avoid custom implementations and use well-established solutions such as RASP (Runtime Application Self-Protection) which can ensure that the API keys are only fully assembled in memory when necessary, keeping them obfuscated or split across different components otherwise. RASP can also dynamically retrieve and manage keys securely at runtime by integrating with secure key management solutions.
