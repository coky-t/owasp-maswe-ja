# OWASP Mobile Application Security Weakness Enumeration ja

- [OWASP Mobile Application Security Weakness Enumeration ja](README.md)

## OWASP モバイルアプリケーションセキュリティ脆弱性タイプ一覧 日本語版

- [モバイルアプリケーションセキュリティ脆弱性タイプ一覧](Document/README.md)

- MASVS-STORAGE: ストレージ
  - [MASWE-0001 プライベートストレージに暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Private Storage)](Document/weaknesses/MASVS-STORAGE/MASWE-0001.md)
  - [MASWE-0002 プライベートストレージの外部に暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted Outside of Private Storage)](Document/weaknesses/MASVS-STORAGE/MASWE-0002.md)
  - [MASWE-0003 プラットフォームキーストアの外部に保存される暗号鍵 (Cryptographic Keys Stored Outside of Platform Keystore)](Document/weaknesses/MASVS-STORAGE/MASWE-0003.md)
  - [MASWE-0004 アプリパッケージ内にハードコードされた機密データ (Sensitive Data Hardcoded in the App Package)](Document/weaknesses/MASVS-STORAGE/MASWE-0004.md)
  - [MASWE-0005 機密データのログへの挿入 (Insertion of Sensitive Data into Logs)](Document/weaknesses/MASVS-STORAGE/MASWE-0005.md)
  - [MASWE-0006 バックアップから除外されない機密データ (Sensitive Data Not Excluded From Backup)](Document/weaknesses/MASVS-STORAGE/MASWE-0006.md)

- MASVS-CRYPTO: 暗号
  - [MASWE-0007 不適切な暗号化 (Improper Encryption)](Document/weaknesses/MASVS-CRYPTO/MASWE-0007.md)
  - [MASWE-0008 不適切なハッシュ化 (Improper Hashing)](Document/weaknesses/MASVS-CRYPTO/MASWE-0008.md)
  - [MASWE-0009 メッセージ認証コード (MAC) の不適切な使用 (Improper Use of Message Authentication Code (MAC))](Document/weaknesses/MASVS-CRYPTO/MASWE-0009.md)
  - [MASWE-0010 暗号署名の不適切な生成 (Improper Generation of Cryptographic Signatures)](Document/weaknesses/MASVS-CRYPTO/MASWE-0010.md)
  - [MASWE-0011 暗号署名の不適切な検証 (Improper Verification of Cryptographic Signature)](Document/weaknesses/MASVS-CRYPTO/MASWE-0011.md)
  - [MASWE-0012 不適切な乱数生成 (Improper Random Number Generation)](Document/weaknesses/MASVS-CRYPTO/MASWE-0012.md)
  - [MASWE-0013 不適切な暗号鍵生成 (Improper Cryptographic Key Generation)](Document/weaknesses/MASVS-CRYPTO/MASWE-0013.md)
  - [MASWE-0014 不適切な暗号鍵導出 (Improper Cryptographic Key Derivation)](Document/weaknesses/MASVS-CRYPTO/MASWE-0014.md)
  - [MASWE-0015 実装されていない暗号鍵ローテーション (Cryptographic Key Rotation Not Implemented)](Document/weaknesses/MASVS-CRYPTO/MASWE-0015.md)
  - [MASWE-0016 制限されていない暗号鍵へのアクセス (Cryptographic Key Access Not Restricted)](Document/weaknesses/MASVS-CRYPTO/MASWE-0016.md)
  - [MASWE-0017 強制されていないデバイスのセキュアロック (Device Secure Lock Not Enforced)](Document/weaknesses/MASVS-CRYPTO/MASWE-0017.md)

- MASVS-AUTH: 認証と認可
  - [MASWE-0018 アプリコンポーネントでの認証や認可の欠如 (Lack of Authentication or Authorization on App Components)](Document/weaknesses/MASVS-AUTH/MASWE-0018.md)
  - [MASWE-0019 クレデンシャルプロバイダに対するオートフィルの欠如 (Lack of Auto-fill Support for Credential Providers)](Document/weaknesses/MASVS-AUTH/MASWE-0019.md)
  - [MASWE-0020 バイパスされる可能性のあるローカル認証 (Local Authentication Can Be Bypassed)](Document/weaknesses/MASVS-AUTH/MASWE-0020.md)
  - [MASWE-0021 機密性の高いトランザクションで許可されている非生体クレデンシャルへのフォールバック (Fallback to Non-biometric Credentials Allowed for Sensitive Transactions)](Document/weaknesses/MASVS-AUTH/MASWE-0021.md)
  - [MASWE-0022 生体要素の新規登録時に無効化されない暗号鍵 (Crypto Keys Not Invalidated on New Biometric Enrollment)](Document/weaknesses/MASVS-AUTH/MASWE-0022.md)
  - [MASWE-0023 機密性の高いアクションで実装されていないステップアップ認証 (Step-Up Authentication Not Implemented for Sensitive Actions)](Document/weaknesses/MASVS-AUTH/MASWE-0023.md)
  - [MASWE-0024 セッション終了後にアクセス可能な機密データ (Sensitive Data Accessible After Session Termination)](Document/weaknesses/MASVS-AUTH/MASWE-0024.md)
  - [MASWE-0025 重要なアクションに対する否認防止の欠如 (Lack of Non-Repudiation for Critical Actions)](Document/weaknesses/MASVS-AUTH/MASWE-0025.md)

- MASVS-NETWORK: ネットワーク通信
  - [MASWE-0026 暗号化されていないネットワークトラフィック (Network Traffic Not Encrypted)](Document/weaknesses/MASVS-NETWORK/MASWE-0026.md)
  - [MASWE-0027 安全でない証明書バリデーション (Insecure Certificate Validation)](Document/weaknesses/MASVS-NETWORK/MASWE-0027.md)
  - [MASWE-0028 安全でないアイデンティティのピン留め (Insecure Identity Pinning)](Document/weaknesses/MASVS-NETWORK/MASWE-0028.md)

- MASVS-PLATFORM: プラットフォーム連携
  - [MASWE-0029 安全でないディープリンク (Insecure Deep Links)](Document/weaknesses/MASVS-PLATFORM/MASWE-0029.md)
  - [MASWE-0030 クリップボードの不適切な使用 (Improper Use of the Clipboard)](Document/weaknesses/MASVS-PLATFORM/MASWE-0030.md)
  - [MASWE-0031 信頼できない App Extension の許可 (Allowing Untrusted App Extensions)](Document/weaknesses/MASVS-PLATFORM/MASWE-0031.md)
  - [MASWE-0032 安全でないインテント (Insecure Intents)](Document/weaknesses/MASVS-PLATFORM/MASWE-0032.md)
  - [MASWE-0033 WebView に公開されている機密性の高いネイティブ機能 (Sensitive Native Functionality Exposed in WebViews)](Document/weaknesses/MASVS-PLATFORM/MASWE-0033.md)
  - [MASWE-0034 信頼できないコンテンツでのローカルリソースへのアクセスを許可する WebView (WebViews Allow Access to Local Resources with Untrusted Content)](Document/weaknesses/MASVS-PLATFORM/MASWE-0034.md)
  - [MASWE-0035 信頼できないコンテンツをロードする WebView (WebViews Loading Untrusted Content)](Document/weaknesses/MASVS-PLATFORM/MASWE-0035.md)
  - [MASWE-0036 ユーザーインタフェースを介した機密データの不必要な露出 (Unnecessary Exposure of Sensitive Data via the User Interface)](Document/weaknesses/MASVS-PLATFORM/MASWE-0036.md)
  - [MASWE-0037 通知を介した機密データの不必要な露出 (Unnecessary Exposure of Sensitive Data via Notifications)](Document/weaknesses/MASVS-PLATFORM/MASWE-0037.md)
  - [MASWE-0038 スクリーンショットまたはスクリーン録画からの機密データの不十分な保護 (Insufficient Protection of Sensitive Data from Screenshots or Screen Recordings)](Document/weaknesses/MASVS-PLATFORM/MASWE-0038.md)
  - [MASWE-0039 オーバーレイ攻撃に脆弱なアプリ (App Vulnerable to Overlay Attacks)](Document/weaknesses/MASVS-PLATFORM/MASWE-0039.md)
  - [MASWE-0040 アクセシビリティサービスを介して漏洩する機密データ (Sensitive Data Leaked via Accessibility Services)](Document/weaknesses/MASVS-PLATFORM/MASWE-0040.md)

- MASVS-CODE: コード品質
  - [MASWE-0041 確保されていない最新のプラットフォームバージョンでの実行 (Running on a Recent Platform Version Not Ensured)](Document/weaknesses/MASVS-CODE/MASWE-0041.md)
  - [MASWE-0042 ターゲットになっていない最新プラットフォームバージョン (Latest Platform Version Not Targeted)](Document/weaknesses/MASVS-CODE/MASWE-0042.md)
  - [MASWE-0043 実装されていない強制アップデート (Enforced Updating Not Implemented)](Document/weaknesses/MASVS-CODE/MASWE-0043.md)
  - [MASWE-0044 既知の脆弱性を持つ依存関係 (Dependencies with Known Vulnerabilities)](Document/weaknesses/MASVS-CODE/MASWE-0044.md)
  - [MASWE-0045 使用されていないコンパイラ提供のセキュリティ機能 (Compiler-Provided Security Features Not Used)](Document/weaknesses/MASVS-CODE/MASWE-0045.md)
  - [MASWE-0046 非推奨の API や機能の使用 (Use of Deprecated APIs or Functionality)](Document/weaknesses/MASVS-CODE/MASWE-0046.md)
  - [MASWE-0047 セキュリティ上重要な機能に対する非標準 API の使用 (Using Non-Standard APIs for Security-Critical Functionality)](Document/weaknesses/MASVS-CODE/MASWE-0047.md)
  - [MASWE-0048 アプリに含まれる悪意のあるコード (Malicious Code Included in the App)](Document/weaknesses/MASVS-CODE/MASWE-0048.md)
  - [MASWE-0049 安全でない動的コードローディング (Unsafe Dynamic Code Loading)](Document/weaknesses/MASVS-CODE/MASWE-0049.md)
  - [MASWE-0050 信頼できないデータの安全でない取り扱い (Unsafe Handling of Untrusted Data)](Document/weaknesses/MASVS-CODE/MASWE-0050.md)

- MASVS-RESILIENCE: リバースエンジニアリングと改竄に対する耐性
  - [MASWE-0051 実装されていないルート/脱獄検出 (Root/Jailbreak Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0051.md)
  - [MASWE-0052 実装されていないアプリ仮想化環境検出 (App Virtualization Environment Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0052.md)
  - [MASWE-0053 実装されていないエミュレートされたデバイスや仮想デバイスの検出 (Emulated or Virtual Device Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0053.md)
  - [MASWE-0054 実装されていない Device Attestation (Device Attestation Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0054.md)
  - [MASWE-0055 実装されていないマルウェア検出 (Malware Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0055.md)
  - [MASWE-0056 実装されていない App Attestation (App Attestation Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0056.md)
  - [MASWE-0057 検証されていないアプリリソースの完全性 (App Resources Integrity Not Verified)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0057.md)
  - [MASWE-0058 検証されていないランタイムコード完全性 (Runtime Code Integrity Not Verified)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0058.md)
  - [MASWE-0059 実装されていないコード難読化 (Code Obfuscation Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0059.md)
  - [MASWE-0060 実装されていないリソース難読化 (Resource Obfuscation Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0060.md)
  - [MASWE-0061 削除されていないデバッグアーティファクト (Debug Artifacts Not Removed)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0061.md)
  - [MASWE-0062 アプリケーションレベルのペイロード暗号化の欠如 (No Application-Level Payload Encryption)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0062.md)
  - [MASWE-0063 無効化されていないデバッグメカニズム (Debug Mechanisms Not Disabled)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0063.md)
  - [MASWE-0064 実装されていないデバッガ検出 (Debugger Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0064.md)
  - [MASWE-0065 実装されていない動的解析ツール検出 (Dynamic Analysis Tools Detection Not Implemented)](Document/weaknesses/MASVS-RESILIENCE/MASWE-0065.md)

- MASVS-PRIVACY: プライバシー
  - [MASWE-0066 不十分なパーミッション管理 (Inadequate Permission Management)](Document/weaknesses/MASVS-PRIVACY/MASWE-0066.md)
  - [MASWE-0067 匿名化対策や仮名化対策の欠如 (Lack of Anonymization or Pseudonymisation Measures)](Document/weaknesses/MASVS-PRIVACY/MASWE-0067.md)
  - [MASWE-0068 ユーザー追跡のための識別子の不適切な使用 (Incorrect Use of Identifiers for User Tracking)](Document/weaknesses/MASVS-PRIVACY/MASWE-0068.md)
  - [MASWE-0069 プライバシー保護が適用されない機能の使用 (Usage of Non-Privacy-Preserving Functionality)](Document/weaknesses/MASVS-PRIVACY/MASWE-0069.md)
  - [MASWE-0070 プライバシー関連アクションに対する不十分な認識 (Inadequate Awareness for Privacy Relevant Actions)](Document/weaknesses/MASVS-PRIVACY/MASWE-0070.md)
  - [MASWE-0071 プライバシー関連アクションに対する不十分なデフォルト (Inadequate Defaults for Privacy Relevant Actions)](Document/weaknesses/MASVS-PRIVACY/MASWE-0071.md)
  - [MASWE-0072 不十分なプライバシーポリシー (Inadequate Privacy Policy)](Document/weaknesses/MASVS-PRIVACY/MASWE-0072.md)
  - [MASWE-0073 不十分なデータ収集宣言 (Inadequate Data Collection Declarations)](Document/weaknesses/MASVS-PRIVACY/MASWE-0073.md)
  - [MASWE-0074 不十分なトラッキングドメイン宣言 (Inadequate Tracking Domains Declarations)](Document/weaknesses/MASVS-PRIVACY/MASWE-0074.md)
  - [MASWE-0075 再現不可能なビルド (Non-Reproducible Builds)](Document/weaknesses/MASVS-PRIVACY/MASWE-0075.md)
  - [MASWE-0076 適切なデータ管理コントロールの欠如 (Lack of Proper Data Management Controls)](Document/weaknesses/MASVS-PRIVACY/MASWE-0076.md)
  - [MASWE-0077 不十分なデータ可視性コントロール (Inadequate Data Visibility Controls)](Document/weaknesses/MASVS-PRIVACY/MASWE-0077.md)
  - [MASWE-0078 不十分または曖昧なユーザー同意メカニズム (Inadequate or Ambiguous User Consent Mechanisms)](Document/weaknesses/MASVS-PRIVACY/MASWE-0078.md)
