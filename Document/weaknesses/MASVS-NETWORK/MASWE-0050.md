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

- **プラットフォーム提供の設定でのクリアテキストトラフィックの許可:** プラットフォーム提供の設定 (Android の Network Security Configuration や iOS の App Transport Security など) を構成して、明示的にクリアテキストトラフィックを許可 (グローバルまたはドメインごとに) し、それらの設定で管理されるすべてのネットワーク接続のデフォルトの動作にします。
- **HTTP の使用:** 通信に HTTPS ではなく HTTP を使用することで、転送時のデータを暗号化しません。
- **HTTP 以外の安全でないプロトコルの使用:** FTP、TLS なしの SMTP、TCP ソケット、転送時のデータを暗号化しないカスタムプロトコルなど、安全でないプロトコルを使用します。
- **低レベルネットワーク API の使用:** Android の `Socket` や iOS の `NSURLConnection` など、暗号化を強制せず、プラットフォームのネットワークセキュリティ設定を尊重しない、低レベルネットワーク API を使用します。
- **クロスプラットフォームフレームワークの構成ミス:** クロスプラットフォームフレームワークの不適切な設定はアプリの Android バージョンと iOS バージョンの両方でクリアテキストトラフィックを許可する可能性があります。
- **サードパーティライブラリ**: デフォルトで安全でない通信手法であったり、不適切な構成となっている、サードパーティライブラリや SDK を使用しています。

## 緩和策

- **安全なプロトコルを使用する:** すべての通信チャネルにおいて HTTPS (暗号化に TLS を採用)、FTPS、SFTP、SMTPS などの安全なプロトコルを常に使用します。これらのプロトコルがアプリ全体で一貫して使用されていることを確保します。
- **クリアテキストトラフィックを明示的に無効化する:** アプリ設定でグローバルにクリアテキストトラフィックを許可してはいけません。Android の Network Security Configuration や iOS の App Transport Security (ATS) などのセキュリティ設定を使用して、クリアテキストトラフィックが明示的に無効化されていることを確保します。グローバル設定よりもドメインごとの例外を優先しますが、他に選択肢がない場合のみ慎重にします。
- **ドメインごとの例外を控えめに使用する:** クリアテキストトラフィックが特定のドメインに絶対に必要な場合は、これらのドメインが信頼されており、アプリの機能に不可欠であることを確認し、それらを含める前に徹底的なリスク評価を実施します。
- **サーバー修正を優先する:** 可能な限り、サーバーチームと協働して安全な通信を可能にします。モバイルアプリにネットワークセキュリティ例外 (クリアテキストトラフィックの許可や TLS 最小バージョンの引き下げなど) を追加するのではなく、有効な証明書と最新の TLS プロトコルで HTTPS をサポートするようにサーバー構成を更新します。
- **高レベルネットワーク API を使用する:** Android の [`HttpsURLConnection`](https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection) や iOS の [`URLSession`](https://developer.apple.com/documentation/foundation/urlsession) など、暗号化、証明書バリデーション、エラーを自動的に処理する高レベルネットワーク API を使用します。プラットフォームが提供するネットワークセキュリティ機能をバイパスする、低レベルネットワーク API やカスタムネットワークスタックを使用することは避けます。
- **安全なクロスプラットフォームフレームワークを使用する:** React Native, Flutter, Xamarin などのクロスプラットフォームフレームワークが、デフォルトで安全な通信を強制し、クリアテキストトラフィックを許可しないように設定されていることを確保します。フレームワークのドキュメントを確認し、ベストプラクティスに沿ってネットワークセキュリティ設定を調整します。
- **安全なサードパーティコンポーネントを使用する:** アプリで使用されるサードパーティライブラリや SDK が、特に機密データを扱う場合や低レベルネットワーク API を使用する場合は、安全な通信プロトコルを適用していることを検証します。これらのコンポーネントが脆弱性に対処するために定期的に更新されていることを確認します。
