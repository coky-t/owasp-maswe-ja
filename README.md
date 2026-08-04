# OWASP Mobile Application Security Weakness Enumeration (MASWE) ja

This is the unofficial Japanese translation of the [OWASP Mobile Application Security Weakness Enumeration (MASWE)](https://github.com/OWASP/maswe).

**!!! Work In Progress !!!**

<!-- - Document Site - <https://coky-t.gitbook.io/owasp-maswe-ja/> -->
- Document Repository - <https://github.com/coky-t/owasp-maswe-ja>

### Originator

- MAS Official Site - <https://mas.owasp.org/>
- Project Site - <https://owasp.org/www-project-mobile-app-security/>
- Project Repository - <https://github.com/OWASP/www-project-mobile-app-security>
- Document Site - <https://mas.owasp.org/MASWE/>
- Document Repository - <https://github.com/OWASP/maswe>

## OWASP モバイルアプリケーションセキュリティ脆弱性タイプ一覧 日本語版

- [モバイルアプリケーションセキュリティ脆弱性タイプ一覧](Document/README.md)

### MASVS-STORAGE: ストレージ

- [MASWE-0001](Document/weaknesses/MASVS-STORAGE/MASWE-0001.md) プライベートストレージに暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Private Storage)
- [MASWE-0002](Document/weaknesses/MASVS-STORAGE/MASWE-0002.md) プライベートストレージの外部に暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted Outside of Private Storage)
- [MASWE-0003](Document/weaknesses/MASVS-STORAGE/MASWE-0003.md) プラットフォームキーストアの外部に保存される暗号鍵 (Cryptographic Keys Stored Outside of Platform Keystore)
- [MASWE-0004](Document/weaknesses/MASVS-STORAGE/MASWE-0004.md) アプリパッケージ内にハードコードされた機密データ (Sensitive Data Hardcoded in the App Package)
- [MASWE-0005](Document/weaknesses/MASVS-STORAGE/MASWE-0005.md) 機密データのログへの挿入 (Insertion of Sensitive Data into Logs)
- [MASWE-0006](Document/weaknesses/MASVS-STORAGE/MASWE-0006.md) バックアップから除外されない機密データ (Sensitive Data Not Excluded From Backup)

### MASVS-CRYPTO: 暗号

- [MASWE-0007](Document/weaknesses/MASVS-CRYPTO/MASWE-0007.md) 不適切な暗号化 (Improper Encryption)
- [MASWE-0008](Document/weaknesses/MASVS-CRYPTO/MASWE-0008.md) 不適切なハッシュ化 (Improper Hashing)
- [MASWE-0009](Document/weaknesses/MASVS-CRYPTO/MASWE-0009.md) メッセージ認証コード (MAC) の不適切な使用 (Improper Use of Message Authentication Code (MAC))
- [MASWE-0010](Document/weaknesses/MASVS-CRYPTO/MASWE-0010.md) 暗号署名の不適切な生成 (Improper Generation of Cryptographic Signatures)
- [MASWE-0011](Document/weaknesses/MASVS-CRYPTO/MASWE-0011.md) 暗号署名の不適切な検証 (Improper Verification of Cryptographic Signature)
- [MASWE-0012](Document/weaknesses/MASVS-CRYPTO/MASWE-0012.md) 不適切な乱数生成 (Improper Random Number Generation)
- [MASWE-0013](Document/weaknesses/MASVS-CRYPTO/MASWE-0013.md) 不適切な暗号鍵生成 (Improper Cryptographic Key Generation)
- [MASWE-0014](Document/weaknesses/MASVS-CRYPTO/MASWE-0014.md) 不適切な暗号鍵導出 (Improper Cryptographic Key Derivation)
- [MASWE-0015](Document/weaknesses/MASVS-CRYPTO/MASWE-0015.md) 実装されていない暗号鍵ローテーション (Cryptographic Key Rotation Not Implemented)
- [MASWE-0016](Document/weaknesses/MASVS-CRYPTO/MASWE-0016.md) 制限されていない暗号鍵へのアクセス (Cryptographic Key Access Not Restricted)
- [MASWE-0017](Document/weaknesses/MASVS-CRYPTO/MASWE-0017.md) 強制されていないデバイスのセキュアロック (Device Secure Lock Not Enforced)

### MASVS-AUTH: 認証と認可

- [MASWE-0018](Document/weaknesses/MASVS-AUTH/MASWE-0018.md) アプリコンポーネントでの認証や認可の欠如 (Lack of Authentication or Authorization on App Components)
- [MASWE-0019](Document/weaknesses/MASVS-AUTH/MASWE-0019.md) クレデンシャルプロバイダに対するオートフィルの欠如 (Lack of Auto-fill Support for Credential Providers)
- [MASWE-0020](Document/weaknesses/MASVS-AUTH/MASWE-0020.md) バイパスされる可能性のあるローカル認証 (Local Authentication Can Be Bypassed)
- [MASWE-0021](Document/weaknesses/MASVS-AUTH/MASWE-0021.md) 機密性の高いトランザクションで許可されている非生体クレデンシャルへのフォールバック (Fallback to Non-biometric Credentials Allowed for Sensitive Transactions)
- [MASWE-0022](Document/weaknesses/MASVS-AUTH/MASWE-0022.md) 生体要素の新規登録時に無効化されない暗号鍵 (Crypto Keys Not Invalidated on New Biometric Enrollment)
- [MASWE-0023](Document/weaknesses/MASVS-AUTH/MASWE-0023.md) 機密性の高いアクションで実装されていないステップアップ認証 (Step-Up Authentication Not Implemented for Sensitive Actions)
- [MASWE-0024](Document/weaknesses/MASVS-AUTH/MASWE-0024.md) セッション終了後にアクセス可能な機密データ (Sensitive Data Accessible After Session Termination)
- [MASWE-0025](Document/weaknesses/MASVS-AUTH/MASWE-0025.md) 重要なアクションに対する否認防止の欠如 (Lack of Non-Repudiation for Critical Actions)

### MASVS-NETWORK: ネットワーク通信

- [MASWE-0026](Document/weaknesses/MASVS-NETWORK/MASWE-0026.md) 暗号化されていないネットワークトラフィック (Network Traffic Not Encrypted)
- [MASWE-0027](Document/weaknesses/MASVS-NETWORK/MASWE-0027.md) 安全でない証明書バリデーション (Insecure Certificate Validation)
- [MASWE-0028](Document/weaknesses/MASVS-NETWORK/MASWE-0028.md) 安全でないアイデンティティのピン留め (Insecure Identity Pinning)

### MASVS-PLATFORM: プラットフォーム連携

- [MASWE-0029](Document/weaknesses/MASVS-PLATFORM/MASWE-0029.md) 安全でないディープリンク (Insecure Deep Links)
- [MASWE-0030](Document/weaknesses/MASVS-PLATFORM/MASWE-0030.md) クリップボードの不適切な使用 (Improper Use of the Clipboard)
- [MASWE-0031](Document/weaknesses/MASVS-PLATFORM/MASWE-0031.md) 信頼できない App Extension の許可 (Allowing Untrusted App Extensions)
- [MASWE-0032](Document/weaknesses/MASVS-PLATFORM/MASWE-0032.md) 安全でないインテント (Insecure Intents)
- [MASWE-0033](Document/weaknesses/MASVS-PLATFORM/MASWE-0033.md) WebView に公開されている機密性の高いネイティブ機能 (Sensitive Native Functionality Exposed in WebViews)
- [MASWE-0034](Document/weaknesses/MASVS-PLATFORM/MASWE-0034.md) 信頼できないコンテンツでのローカルリソースへのアクセスを許可する WebView (WebViews Allow Access to Local Resources with Untrusted Content)
- [MASWE-0035](Document/weaknesses/MASVS-PLATFORM/MASWE-0035.md) 信頼できないコンテンツをロードする WebView (WebViews Loading Untrusted Content)
- [MASWE-0036](Document/weaknesses/MASVS-PLATFORM/MASWE-0036.md) ユーザーインタフェースを介した機密データの不必要な露出 (Unnecessary Exposure of Sensitive Data via the User Interface)
- [MASWE-0037](Document/weaknesses/MASVS-PLATFORM/MASWE-0037.md) 通知を介した機密データの不必要な露出 (Unnecessary Exposure of Sensitive Data via Notifications)
- [MASWE-0038](Document/weaknesses/MASVS-PLATFORM/MASWE-0038.md) スクリーンショットまたはスクリーン録画からの機密データの不十分な保護 (Insufficient Protection of Sensitive Data from Screenshots or Screen Recordings)
- [MASWE-0039](Document/weaknesses/MASVS-PLATFORM/MASWE-0039.md) オーバーレイ攻撃に脆弱なアプリ (App Vulnerable to Overlay Attacks)
- [MASWE-0040](Document/weaknesses/MASVS-PLATFORM/MASWE-0040.md) アクセシビリティサービスを介して漏洩する機密データ (Sensitive Data Leaked via Accessibility Services)

### MASVS-CODE: コード品質

- [MASWE-0041](Document/weaknesses/MASVS-CODE/MASWE-0041.md) 確保されていない最新のプラットフォームバージョンでの実行 (Running on a Recent Platform Version Not Ensured)
- [MASWE-0042](Document/weaknesses/MASVS-CODE/MASWE-0042.md) ターゲットになっていない最新プラットフォームバージョン (Latest Platform Version Not Targeted)
- [MASWE-0043](Document/weaknesses/MASVS-CODE/MASWE-0043.md) 実装されていない強制アップデート (Enforced Updating Not Implemented)
- [MASWE-0044](Document/weaknesses/MASVS-CODE/MASWE-0044.md) 既知の脆弱性を持つ依存関係 (Dependencies with Known Vulnerabilities)
- [MASWE-0045](Document/weaknesses/MASVS-CODE/MASWE-0045.md) 使用されていないコンパイラ提供のセキュリティ機能 (Compiler-Provided Security Features Not Used)
- [MASWE-0046](Document/weaknesses/MASVS-CODE/MASWE-0046.md) 非推奨の API や機能の使用 (Use of Deprecated APIs or Functionality)
- [MASWE-0047](Document/weaknesses/MASVS-CODE/MASWE-0047.md) セキュリティ上重要な機能に対する非標準 API の使用 (Using Non-Standard APIs for Security-Critical Functionality)
- [MASWE-0048](Document/weaknesses/MASVS-CODE/MASWE-0048.md) アプリに含まれる悪意のあるコード (Malicious Code Included in the App)
- [MASWE-0049](Document/weaknesses/MASVS-CODE/MASWE-0049.md) 安全でない動的コードローディング (Unsafe Dynamic Code Loading)
- [MASWE-0050](Document/weaknesses/MASVS-CODE/MASWE-0050.md) 信頼できないデータの安全でない取り扱い (Unsafe Handling of Untrusted Data)

### MASVS-RESILIENCE: リバースエンジニアリングと改竄に対する耐性

- [MASWE-0051](Document/weaknesses/MASVS-RESILIENCE/MASWE-0051.md) 実装されていないルート/脱獄検出 (Root/Jailbreak Detection Not Implemented)
- [MASWE-0052](Document/weaknesses/MASVS-RESILIENCE/MASWE-0052.md) 実装されていないアプリ仮想化環境検出 (App Virtualization Environment Detection Not Implemented)
- [MASWE-0053](Document/weaknesses/MASVS-RESILIENCE/MASWE-0053.md) 実装されていないエミュレートされたデバイスや仮想デバイスの検出 (Emulated or Virtual Device Detection Not Implemented)
- [MASWE-0054](Document/weaknesses/MASVS-RESILIENCE/MASWE-0054.md) 実装されていない Device Attestation (Device Attestation Not Implemented)
- [MASWE-0055](Document/weaknesses/MASVS-RESILIENCE/MASWE-0055.md) 実装されていないマルウェア検出 (Malware Detection Not Implemented)
- [MASWE-0056](Document/weaknesses/MASVS-RESILIENCE/MASWE-0056.md) 実装されていない App Attestation (App Attestation Not Implemented)
- [MASWE-0057](Document/weaknesses/MASVS-RESILIENCE/MASWE-0057.md) 検証されていないアプリリソースの完全性 (App Resources Integrity Not Verified)
- [MASWE-0058](Document/weaknesses/MASVS-RESILIENCE/MASWE-0058.md) 検証されていないランタイムコード完全性 (Runtime Code Integrity Not Verified)
- [MASWE-0059](Document/weaknesses/MASVS-RESILIENCE/MASWE-0059.md) 実装されていないコード難読化 (Code Obfuscation Not Implemented)
- [MASWE-0060](Document/weaknesses/MASVS-RESILIENCE/MASWE-0060.md) 実装されていないリソース難読化 (Resource Obfuscation Not Implemented)
- [MASWE-0061](Document/weaknesses/MASVS-RESILIENCE/MASWE-0061.md) 削除されていないデバッグアーティファクト (Debug Artifacts Not Removed)
- [MASWE-0062](Document/weaknesses/MASVS-RESILIENCE/MASWE-0062.md) アプリケーションレベルのペイロード暗号化の欠如 (No Application-Level Payload Encryption)
- [MASWE-0063](Document/weaknesses/MASVS-RESILIENCE/MASWE-0063.md) 無効化されていないデバッグメカニズム (Debug Mechanisms Not Disabled)
- [MASWE-0064](Document/weaknesses/MASVS-RESILIENCE/MASWE-0064.md) 実装されていないデバッガ検出 (Debugger Detection Not Implemented)
- [MASWE-0065](Document/weaknesses/MASVS-RESILIENCE/MASWE-0065.md) 実装されていない動的解析ツール検出 (Dynamic Analysis Tools Detection Not Implemented)

### MASVS-PRIVACY: プライバシー

- [MASWE-0066](Document/weaknesses/MASVS-PRIVACY/MASWE-0066.md) 不十分なパーミッション管理 (Inadequate Permission Management)
- [MASWE-0067](Document/weaknesses/MASVS-PRIVACY/MASWE-0067.md) 匿名化対策や仮名化対策の欠如 (Lack of Anonymization or Pseudonymisation Measures)
- [MASWE-0068](Document/weaknesses/MASVS-PRIVACY/MASWE-0068.md) ユーザー追跡のための識別子の不適切な使用 (Incorrect Use of Identifiers for User Tracking)
- [MASWE-0069](Document/weaknesses/MASVS-PRIVACY/MASWE-0069.md) プライバシー保護が適用されない機能の使用 (Usage of Non-Privacy-Preserving Functionality)
- [MASWE-0070](Document/weaknesses/MASVS-PRIVACY/MASWE-0070.md) プライバシー関連アクションに対する不十分な認識 (Inadequate Awareness for Privacy Relevant Actions)
- [MASWE-0071](Document/weaknesses/MASVS-PRIVACY/MASWE-0071.md) プライバシー関連アクションに対する不十分なデフォルト (Inadequate Defaults for Privacy Relevant Actions)
- [MASWE-0072](Document/weaknesses/MASVS-PRIVACY/MASWE-0072.md) 不十分なプライバシーポリシー (Inadequate Privacy Policy)
- [MASWE-0073](Document/weaknesses/MASVS-PRIVACY/MASWE-0073.md) 不十分なデータ収集宣言 (Inadequate Data Collection Declarations)
- [MASWE-0074](Document/weaknesses/MASVS-PRIVACY/MASWE-0074.md) 不十分なトラッキングドメイン宣言 (Inadequate Tracking Domains Declarations)
- [MASWE-0075](Document/weaknesses/MASVS-PRIVACY/MASWE-0075.md) 再現不可能なビルド (Non-Reproducible Builds)
- [MASWE-0076](Document/weaknesses/MASVS-PRIVACY/MASWE-0076.md) 適切なデータ管理コントロールの欠如 (Lack of Proper Data Management Controls)
- [MASWE-0077](Document/weaknesses/MASVS-PRIVACY/MASWE-0077.md) 不十分なデータ可視性コントロール (Inadequate Data Visibility Controls)
- [MASWE-0078](Document/weaknesses/MASVS-PRIVACY/MASWE-0078.md) 不十分または曖昧なユーザー同意メカニズム (Inadequate or Ambiguous User Consent Mechanisms)

## License

[Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/)

## Translator (Japanese)

[Koki Takeyama](https://github.com/coky-t)

<!-- - Document Site - <https://coky-t.gitbook.io/owasp-docs-ja/> -->
- Document Repository - <https://github.com/coky-t/owasp-docs-ja>
