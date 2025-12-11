---
title: 安全でない証明書検証 (Insecure Certificate Validation)
id: MASWE-0052
alias: insecure-cert-val
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-NETWORK-3]
  masvs-v2: [MASVS-NETWORK-1]
  cwe: [295, 297]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/unsafe-trustmanager
  - https://developer.android.com/privacy-and-security/risks/unsafe-hostname
refs:
  - https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-52r2.pdf#page=17
  - https://developer.android.com/privacy-and-security/security-ssl#tls-1.3-enabled-by-default
  - https://support.google.com/faqs/answer/7071387?hl=en
  - https://developer.android.com/reference/android/webkit/WebViewClient.html?sjid=15211564825735678155-EU#onReceivedSslError(android.webkit.WebView,%20android.webkit.SslErrorHandler,%20android.net.http.SslError)
  - https://developer.android.com/privacy-and-security/security-ssl#WarningsSslSocket
  - https://wiki.sei.cmu.edu/confluence/display/java/MSC00-J.+Use+SSLSocket+rather+than+Socket+for+secure+data+exchange
status: new
---

## 概要

安全な通信時に TLS 証明書を適切に検証しないアプリは [中間マシン (MITM)](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04f-Testing-Network-Communication.md#intercepting-network-traffic-through-mitm) 攻撃やその他のセキュリティ脅威の影響を受けやすくなります。この弱点は、アプリが無効な証明書、期限切れの証明書、自己署名証明書、または信頼できない証明書を適切な検証なしに受け入れる場合に発生し、転送時のデータの完全性と機密性を損ないます。

## 影響

- **データ傍受**: 攻撃者はネットワーク経由で伝達される機密情報を捕捉して読み取ることができます。
- **データ操作**: 攻撃者は転送中のデータを改変し、破損を引き起こしたり、悪意のあるコンテンツを注入する可能性があります。
- **データ露出**: 機密情報が侵害される可能性があります。
- **不正アクセス**: 攻撃者は認証トークンやクレデンシャルを傍受することで、ユーザーアカウントやシステムに不正アクセスを獲得する可能性があります。
- **サービスのなりすまし**: ユーザーは正当なサービスを装う悪意のあるサーバーとやり取りするように誘導される可能性があります。
- **データ完全性の喪失**: 改変または破損したデータがアプリケーションに受け入れられ、信頼性の低い結果や悪意のある結果につながる可能性があります。

## 流入の形態

- **証明書バリデーションの無効化**: 開発者は、開発を簡素化したり、接続の問題をトラブルシュートするために、証明書バリデーションチェックを無効またはバイパスします。
- **自己署名証明書の受入**: アプリケーションは信頼できる認証局 (CA) による適切なバリデーションなしで自己署名証明書や信頼できない証明書を受け入れます。
- **ホスト名検証の無視**: 証明書のホスト名がサーバーのホスト名と一致することを検証しないと、攻撃者が他のドメインの有効な証明書を提示できます。
- **安全でないカスタムトラストマネージャの使用**: 不完全、不正確、または安全でないカスタム証明書バリデーションロジックを実装します。
- **不適切なエラー処理**: 証明書バリデーションエラーが発生しても、ユーザーに警告したり接続を終了したりせずに、接続を続行します。
- **すべての証明書を信頼**: バリデーションなしで、デフォルトですべての証明書を信頼するようにアプリケーションを構成します。

## 緩和策

- **Enforce Strict Certificate Validation**: Always validate TLS certificates against a trusted set of Certificate Authorities (CAs) provided by the operating system or a trusted third party.
- **Avoid Accepting Self-Signed Certificates**: Do not accept self-signed or untrusted certificates in production environments unless there is a secure mechanism to trust them explicitly.
- **Enable Hostname Verification**: Ensure that the application's network layer verifies the server's hostname against the certificate's Subject Alternative Name (SAN) or Common Name (CN).
- **Use Standard Trust Managers**: Utilize well-established libraries and platform-provided APIs for certificate validation instead of custom implementations.
- **Handle Validation Errors Properly**: Terminate the connection and alert the user whenever certificate validation fails due to issues like expiration, revocation, or mismatch.
