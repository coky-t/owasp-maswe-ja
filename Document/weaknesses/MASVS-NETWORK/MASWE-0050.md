---
title: クリアテキストトラフィック (Cleartext Traffic)
id: MASWE-0050
alias: cleartext-traffic
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-NETWORK-2]
  masvs-v2: [MASVS-NETWORK-1]
  cwe: [319]
  android-risks:
    - https://developer.android.com/privacy-and-security/risks/cleartext-communications
  android-core-app-quality: [SC-9, SC-N1, SC-N2]
refs:
- https://developer.apple.com/documentation/security/preventing-insecure-network-connections
- https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity/nsexceptiondomains
- https://developer.apple.com/documentation/network
- https://developer.apple.com/documentation/foundation/urlsession
- https://developer.android.com/privacy-and-security/security-best-practices#secure-communication
- https://developer.android.com/privacy-and-security/security-tips#networking
- https://developer.android.com/privacy-and-security/security-config#CleartextTrafficPermitted
- https://developer.android.com/reference/javax/net/ssl/SSLSocket
- https://developer.android.com/reference/android/security/NetworkSecurityPolicy#isCleartextTrafficPermitted()
- https://developer.android.com/reference/java/net/Socket
- https://developer.android.com/reference/android/webkit/WebView
- https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection
- https://github.com/MicrosoftDocs/xamarin-docs/blob/live/docs/android/app-fundamentals/http-stack.md
- https://github.com/MicrosoftDocs/xamarin-docs/blob/live/docs/ios/app-fundamentals/ats.md
status: new
---

## 概要

データがクリアテキスト (つまり暗号化なし) で送信されると、ネットワークチャネルを監視できる攻撃者がアクセス可能になります。攻撃者は、受動的な盗聴を実行してデータを傍受したり、能動的な [中間マシン (MITM)](https://github.com/coky-t/owasp-mastg-ja/blob/master/Document/0x04f-Testing-Network-Communication.md#intercepting-network-traffic-through-mitm) 攻撃を使用してデータを操作し、アプリの動作を改変したり、悪意のあるコンテンツを注入する可能性があります。

この弱点は、機密情報が暗号化なしで送信される場合に特に懸念され、ユーザーのプライバシーとセキュリティが直接的なリスクにされされます。機密データが送信されていない場合でも、クリアテキスト通信を使用することは脆弱性を残します。ARP ポイズニングや DNS スプーフィングなどのネットワーク攻撃は、攻撃者がトラフィックを傍受またはリダイレクトすることを可能にして、アプリ機能を妨害したり、正規のサービスを装う悪意のあるサイトにリダイレクトしてユーザーを欺く可能性があります。

接続が暗号化と適切な認証メカニズムを使用して保護されていれば、攻撃者は暗号化と証明書バリデーションをバイパスする必要があるため、これらの攻撃は実行がはるかに困難になります。安全なネットワークプロトコルは、機密性を提供するだけでなく、暗号化と証明書バリデーションを通じてデータの完全性と真正性も確保し、攻撃者がデータを改竄することを防ぎます。

## 影響

- **データ傍受**: 攻撃者はネットワークで送信される機密情報をキャプチャして読み取ることができます。
- **データ操作**: 攻撃者は転送時のデータを改竄し、破損を引き起こしたり、悪意のあるコンテンツを注入する可能性があります。
- **不正アクセス**: 攻撃者はクリアテキストチャネルで送信されたセッショントークンやクレデンシャルを傍受し、ユーザーを騙してユーザーアカウントやシステムに不正にアクセスできる可能性があります。
- **プライバシー侵害**: 個人情報と機密性の高いユーザー情報が露出し、プライバシー規制に違反する可能性があります。
- **規制コンプライアンス違反**: 機密データの露出は GDPR や HIPAA などの法律の非準拠につながり、法的罰則をもたらす可能性があります。
- **評判の失墜**: セキュリティ侵害はユーザーの信頼を損ない、組織の評判を害する可能性があります。

## 流入の形態

- **Cleartext Traffic Allowed in Platform-provided Settings:** Configuring platform-provided settings (e.g. Network Security Configuration on Android or App Transport Security on iOS) to explicitly allow cleartext traffic (globally or per-domain), making it the default behavior for all network connections managed by those settings.
- **Usage of HTTP:** Using HTTP instead of HTTPS for communication, which does not encrypt data in transit.
- **Usage of Non-HTTP Insecure Protocols:** Using insecure protocols such as FTP, SMTP without TLS, TCP sockets or custom protocols which do not encrypt data in transit.
- **Usage of Low-Level Network APIs:** Use of low-level network APIs that do not enforce encryption and do not honor the platform's network security settings, such as `Socket` on Android or `NSURLConnection` on iOS.
- **Cross-Platform Framework Misconfiguration:** Improper settings in cross-platform frameworks may allow cleartext traffic for both Android and iOS versions of an app.
- **Third-Party Libraries**: Using third-party libraries or SDKs that default to insecure communication methods or are improperly configured.

## 緩和策

- **Use Secure Protocols:** Always use secure protocols like HTTPS (which employs TLS for encryption), FTPS, SFTP or SMTPS for all communication channels. Ensure these protocols are used consistently throughout the app.
- **Explicitly Disable Cleartext Traffic:** Never allow cleartext traffic globally in the app configuration. Ensure that cleartext traffic is explicitly disabled using security settings like the Network Security Configuration on Android and App Transport Security (ATS) on iOS. Prefer per-domain exceptions over global settings but use them carefully and only when there is no other option.
- **Use Per-Domain Exceptions Sparingly:** If cleartext traffic is absolutely necessary for specific domains, ensure these domains are trusted and essential for the app's functionality, and conduct a thorough risk assessment before including them.
- **Prefer Server Fixes**: Whenever possible, work with the server team to enable secure communication. Instead of adding network security exceptions to the mobile app, such as allowing cleartext traffic or lowering the minimum TLS version, update server configurations to support HTTPS with valid certificates and modern TLS protocols.
- **Use High-Level Network APIs:** Use high-level network APIs that automatically handle encryption, certificate validation, and errors, such as [`HttpsURLConnection`](https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection) on Android or [`URLSession`](https://developer.apple.com/documentation/foundation/urlsession) on iOS. Avoid using low-level network APIs or custom network stacks that bypass the platform-provided network security features.
- **Use Secure Cross-Platform Frameworks:** Ensure that cross-platform frameworks—such as React Native, Flutter, or Xamarin—are configured to enforce secure communication by default and do not allow cleartext traffic. Review the framework's documentation and adjust network security settings to align with best practices.
- **Use Secure Third-Party Components**: Verify that any third-party libraries and SDKs used in the app enforce secure communication protocols, especially if they handle sensitive data or use low-level networking APIs. Ensure that these components are regularly updated to address any vulnerabilities.
