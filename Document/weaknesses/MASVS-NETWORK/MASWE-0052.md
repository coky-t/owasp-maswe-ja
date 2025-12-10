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

- **Disabling Certificate Validation**: Developers disable or bypass certificate validation checks to simplify development or troubleshoot connectivity issues.
- **Accepting Self-Signed Certificates**: Applications accept self-signed or untrusted certificates without proper validation against trusted Certificate Authorities (CAs).
- **Ignoring Hostname Verification**: Failing to verify that the certificate's hostname matches the server's hostname allows attackers to present valid certificates for other domains.
- **Using Insecure Custom Trust Managers**: Implementing custom certificate validation logic that is incomplete, incorrect, or insecure.
- **Incorrect Error Handling**: Proceeding with connections even when certificate validation errors occur, without alerting the user or terminating the connection.
- **Trusting All Certificates**: Configuring the application to trust all certificates by default, without any validation.

## 緩和策

- **Enforce Strict Certificate Validation**: Always validate TLS certificates against a trusted set of Certificate Authorities (CAs) provided by the operating system or a trusted third party.
- **Avoid Accepting Self-Signed Certificates**: Do not accept self-signed or untrusted certificates in production environments unless there is a secure mechanism to trust them explicitly.
- **Enable Hostname Verification**: Ensure that the application's network layer verifies the server's hostname against the certificate's Subject Alternative Name (SAN) or Common Name (CN).
- **Use Standard Trust Managers**: Utilize well-established libraries and platform-provided APIs for certificate validation instead of custom implementations.
- **Handle Validation Errors Properly**: Terminate the connection and alert the user whenever certificate validation fails due to issues like expiration, revocation, or mismatch.
