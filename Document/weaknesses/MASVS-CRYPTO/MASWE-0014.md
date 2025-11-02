---
title: 保存時に適切に保護されていない暗号鍵 (Cryptographic Keys Not Properly Protected at Rest)
id: MASWE-0014
alias: crypto-keys-not-protected-at-rest
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-STORAGE-1]
  masvs-v2: [MASVS-CRYPTO-2, MASVS-STORAGE-1]
  cwe: [312, 318, 321]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/hardcoded-cryptographic-secrets
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf
status: new
---

## 概要

暗号鍵はモバイルアプリケーションの機密データを保護するために不可欠です。しかし、これらの鍵が保存時に適切に保護されていない場合、簡単に侵害される可能性があります。この弱点は、暗号化されていない SharedPreferences、保護されていないファイルなどの安全でない場所に暗号鍵を保存したり、アプリケーションコード内にハードコードしたり、ソース管理システムやバージョン管理システムに含めることで最終的に本番のアプリケーションパッケージに組み込まれる可能性があることに起因します。

攻撃者はアプリを逆コンパイルやリバースエンジニアして、ハードコードされた鍵を抽出できます。

## 影響

- **不正アクセス**: 暗号鍵が適切に保護されていない場合、攻撃者は機密データに不正アクセスし、アイデンティティ窃取の可能性があります。
- **完全性の喪失**: 鍵が侵害されると、攻撃者は暗号化されたデータを改竄できる可能性があります。
- **機密性の喪失**: 機密情報がさらされると、機密性の喪失をもたらす可能性があります。鍵がさらされると、その鍵で暗号化されたすべてのデータが危険にさらされます。

## 流入の形態

- **安全でない保存場所**: 安全な保管用に設計されていない場所に暗号鍵を保存すること。通常の構成ファイルやユーザー設定ファイル、アプリケーションデータディレクトリ、暗号化およびアクセス制御メカニズムがないその他の領域など。
- **ハードコードされた鍵**: アプリケーションコードに暗号鍵を直接含めること。逆コンパイルやリバースエンジニアリングを通じて抽出の影響を受けやすくなります。
- **暗号化の欠如**: 安全な手法を使用した暗号化なしで、暗号鍵を平文にエクスポートすること。

## 緩和策

- **プラットフォームのキーストアを使用する**: 可能な場合、事前定義された鍵を使用するのではなく、デバイス上で動的に暗号鍵を生成し、作成後は安全に保存するようにします。これには、[Android KeyStore](https://developer.android.com/training/articles/keystore) や [iOS KeyChain](https://developer.apple.com/documentation/security/keychain_services) などのプラットフォーム固有のキーストアを使用できます。
- **最強のハードウェアセキュリティソリューションを実装する**: 最も重要なケースで、かつ現在のユースケースで [利用可能かつ互換性がある](https://developer.android.com/privacy-and-security/keystore#HardwareSecurityModule) 場合はいつでも、[Android StrongBox](https://source.android.com/docs/security/features/keystore/strongbox) や  iOS の Secure Enclave [`kSecAttrTokenIDSecureEnclave`](https://developer.apple.com/documentation/security/ksecattrtokenidsecureenclave) オプションなどの最強のハードウェア基盤のセキュリティオプションを活用して、物理攻撃やサイドチャネル攻撃を含む最高の保護を確保します。
- **暗号鍵管理システムを使用する**: 機密データの安全な保管、アクセス制御、監査機能を提供するサーバーサイドサービスから安全に鍵を取得します。たとえば、AWS Secrets Manager, Azure Key Vault, Google Cloud Secret Manager は一般的なマネージドシークレットストレージソリューションです。アプリは安全で認証された API 呼び出しを通じて、実行時に必要なシークレットを安全に取得できます。
- **鍵を暗号化とラップする**: プラットフォームのキーストアに鍵を保存することがユースケースに適していない場合、または鍵をエクスポートする必要がある場合、[NIST.SP.800-175Br1 5.3.5](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175Br1.pdf) で指定されているエンベロープ暗号 (DEK+KEK) と鍵ラッピング技法を使用して、暗号鍵を保存前に保護します。
- **標準的な鍵管理のベストプラクティスに準拠する**: [NIST.SP.800-57pt1r5 6.2.2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf) に概説されているように、鍵ローテーションやストレージ内の鍵の堅牢な保護メカニズムなどの適切な鍵管理プラクティスを実装し、可用性、完全性、機密性、および使用状況、エンティティ、関連情報との適切な関連付けを確保します。
