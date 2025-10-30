# OWASP Mobile Application Security Weakness Enumeration (MASWE) ja

This is the unofficial Japanese translation of the [OWASP Mobile Application Security Weakness Enumeration (MASWE)](https://github.com/OWASP/maswe).

**!!! Work In Progress !!!**

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

- [MASWE-0001](Document/weaknesses/MASVS-STORAGE/MASWE-0001.md) 機密データのログへの挿入 (Insertion of Sensitive Data into Logs)
- [MASWE-0002](Document/weaknesses/MASVS-STORAGE/MASWE-0002.md) 内部の場所に不十分なアクセス制限で保存された機密データ (Sensitive Data Stored With Insufficient Access Restrictions in Internal Locations)
- [MASWE-0003](Document/weaknesses/MASVS-STORAGE/MASWE-0003.md) 暗号化されていないバックアップ (Backup Unencrypted)
- [MASWE-0004](Document/weaknesses/MASVS-STORAGE/MASWE-0004.md) バックアップから除外されない機密データ (Sensitive Data Not Excluded From Backup)
- [MASWE-0006](Document/weaknesses/MASVS-STORAGE/MASWE-0006.md) プライベートストレージの場所に暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Private Storage Locations)
- [MASWE-0007](Document/weaknesses/MASVS-STORAGE/MASWE-0007.md) ユーザーの介入を必要としない共有ストレージに暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Shared Storage Requiring No User Interaction)

### MASVS-CRYPTO: 暗号

- [MASWE-0009](Document/weaknesses/MASVS-CRYPTO/MASWE-0009.md) 不適切な暗号鍵生成 (Improper Cryptographic Key Generation)
- [MASWE-0010](Document/weaknesses/MASVS-CRYPTO/MASWE-0010.md) 不適切な暗号鍵導出 (Improper Cryptographic Key Derivation)
- [MASWE-0011](Document/weaknesses/MASVS-CRYPTO/MASWE-0011.md) 実装されていない暗号鍵ローテーション (Cryptographic Key Rotation Not Implemented)
- [MASWE-0012](Document/weaknesses/MASVS-CRYPTO/MASWE-0012.md) 暗号鍵の安全でない使用法や誤った使用法 (Insecure or Wrong Usage of Cryptographic Key)
- [MASWE-0013](Document/weaknesses/MASVS-CRYPTO/MASWE-0013.md) ハードコードされた暗号鍵の使用 (Hardcoded Cryptographic Keys in Use)
- [MASWE-0014](Document/weaknesses/MASVS-CRYPTO/MASWE-0014.md) 保存時に適切に保護されていない暗号鍵 (Cryptographic Keys Not Properly Protected at Rest)
- [MASWE-0015](Document/weaknesses/MASVS-CRYPTO/MASWE-0015.md) 非推奨の Android KeyStore 実装 (Deprecated Android KeyStore Implementations)
- [MASWE-0016](Document/weaknesses/MASVS-CRYPTO/MASWE-0016.md) インポートされた暗号鍵の安全でない取り扱い (Unsafe Handling of Imported Cryptographic Keys)
- [MASWE-0017](Document/weaknesses/MASVS-CRYPTO/MASWE-0017.md) エクスポート時に適切に保護されていない暗号鍵 (Cryptographic Keys Not Properly Protected on Export)
- [MASWE-0018](Document/weaknesses/MASVS-CRYPTO/MASWE-0018.md) 制限されていない暗号鍵へのアクセス (Cryptographic Keys Access Not Restricted)
- [MASWE-0019](Document/weaknesses/MASVS-CRYPTO/MASWE-0019.md) リスクのある暗号実装 (Risky Cryptography Implementations)
- [MASWE-0020](Document/weaknesses/MASVS-CRYPTO/MASWE-0020.md) 不適切な暗号化 (Improper Encryption)
- [MASWE-0021](Document/weaknesses/MASVS-CRYPTO/MASWE-0021.md) 不適切なハッシュ化 (Improper Hashing)
- [MASWE-0022](Document/weaknesses/MASVS-CRYPTO/MASWE-0022.md) 予測可能な初期化ベクトル (IV) (Predictable Initialization Vectors (IVs))
- [MASWE-0023](Document/weaknesses/MASVS-CRYPTO/MASWE-0023.md) リスクのあるパディング (Risky Padding)
- [MASWE-0024](Document/weaknesses/MASVS-CRYPTO/MASWE-0024.md) メッセージ認証コード (MAC) の不適切な使用 (Improper Use of Message Authentication Code (MAC))
- [MASWE-0025](Document/weaknesses/MASVS-CRYPTO/MASWE-0025.md) 暗号署名の不適切な生成 (Improper Generation of Cryptographic Signatures)
- [MASWE-0026](Document/weaknesses/MASVS-CRYPTO/MASWE-0026.md) 暗号署名の不適切な検証 (Improper Verification of Cryptographic Signature)
- [MASWE-0027](Document/weaknesses/MASVS-CRYPTO/MASWE-0027.md) 不適切な乱数生成 (Improper Random Number Generation)

### MASVS-AUTH: 認証と認可

- [MASWE-0005](Document/weaknesses/MASVS-AUTH/MASWE-0005.md) アプリパッケージにハードコードされた API キー (API Keys Hardcoded in the App Package)
- [MASWE-0028](Document/weaknesses/MASVS-AUTH/MASWE-0028.md) ベストプラクティスに従っていない MFA 実装 (MFA Implementation Best Practices Not Followed)
- [MASWE-0029](Document/weaknesses/MASVS-AUTH/MASWE-0029.md) 実装されていないログイン後のステップアップ認証 (Step-Up Authentication Not Implemented After Login)
- [MASWE-0030](Document/weaknesses/MASVS-AUTH/MASWE-0030.md) コンテキストの状態変化でトリガーされない再認証 (Re-Authenticates Not Triggered On Contextual State Changes)
- [MASWE-0031](Document/weaknesses/MASVS-AUTH/MASWE-0031.md) Android Protected Confirmation の安全でない使用 (Insecure use of Android Protected Confirmation)
- [MASWE-0032](Document/weaknesses/MASVS-AUTH/MASWE-0032.md) 使用されていないプラットフォームが提供する認証 API (Platform-provided Authentication APIs Not Used)
- [MASWE-0033](Document/weaknesses/MASVS-AUTH/MASWE-0033.md) セキュリティベストプラクティスに従っていない認証または認可プロトコル (Authentication or Authorization Protocol Security Best Practices Not Followed)
- [MASWE-0034](Document/weaknesses/MASVS-AUTH/MASWE-0034.md) クレデンシャル確認の安全でない認証 (Insecure Implementation of Confirm Credentials)
- [MASWE-0035](Document/weaknesses/MASVS-AUTH/MASWE-0035.md) 実装されていないパスワードレス認証 (Passwordless Authentication Not Implemented)
- [MASWE-0036](Document/weaknesses/MASVS-AUTH/MASWE-0036.md) デバイス上に暗号化されずに保存される認証マテリアル (Authentication Material Stored Unencrypted on the Device)
- [MASWE-0037](Document/weaknesses/MASVS-AUTH/MASWE-0037.md) 安全でない接続で送信される認証マテリアル (Authentication Material Sent over Insecure Connections)
- [MASWE-0038](Document/weaknesses/MASVS-AUTH/MASWE-0038.md) 検証されていない認証トークン (Authentication Tokens Not Validated)
- [MASWE-0039](Document/weaknesses/MASVS-AUTH/MASWE-0039.md) 実装されていない共有ウェブクレデンシャルとウェブサイトの関連付け (Shared Web Credentials and Website-association Not Implemented)
- [MASWE-0040](Document/weaknesses/MASVS-AUTH/MASWE-0040.md) WebView における安全でない認証 (Insecure Authentication in WebViews)
- [MASWE-0041](Document/weaknesses/MASVS-AUTH/MASWE-0041.md) サーバーサイドではなくローカルでのみ実施される認証 (Authentication Enforced Only Locally Instead of on the Server-side)
- [MASWE-0042](Document/weaknesses/MASVS-AUTH/MASWE-0042.md) サーバーサイドではなくローカルでのみ実施される認可 (Authorization Enforced Only Locally Instead of on the Server-side)
- [MASWE-0043](Document/weaknesses/MASVS-AUTH/MASWE-0043.md) プラットフォームの KeyStore にバインドされていないアプリのカスタム PIN (App Custom PIN Not Bound to Platform KeyStore)
- [MASWE-0044](Document/weaknesses/MASVS-AUTH/MASWE-0044.md) バイパスされる可能性がある生体認証 (Biometric Authentication Can Be Bypassed)
- [MASWE-0045](Document/weaknesses/MASVS-AUTH/MASWE-0045.md) 機密性の高いトランザクションで許可されている非生体クレデンシャルへのフォールバック (Fallback to Non-biometric Credentials Allowed for Sensitive Transactions)
- [MASWE-0046](Document/weaknesses/MASVS-AUTH/MASWE-0046.md) 生体要素の新規登録時に無効化されない暗号鍵 (Crypto Keys Not Invalidated on New Biometric Enrollment)

### MASVS-NETWORK: ネットワーク通信

- [MASWE-0047](Document/weaknesses/MASVS-NETWORK/MASWE-0047.md) 安全でないアイデンティティのピン留め (Insecure Identity Pinning)
- [MASWE-0048](Document/weaknesses/MASVS-NETWORK/MASWE-0048.md) 安全でないマシン間通信 (Insecure Machine-to-Machine Communication)
- [MASWE-0049](Document/weaknesses/MASVS-NETWORK/MASWE-0049.md) 使用されていない実証済みネットワーク API (Proven Networking APIs Not used)
- [MASWE-0050](Document/weaknesses/MASVS-NETWORK/MASWE-0050.md) クリアテキストトラフィック (Cleartext Traffic)
- [MASWE-0051](Document/weaknesses/MASVS-NETWORK/MASWE-0051.md) 保護されていないオープンポート (Unprotected Open Ports)
- [MASWE-0052](Document/weaknesses/MASVS-NETWORK/MASWE-0052.md) 安全でない証明書検証 (Insecure Certificate Validation)

### MASVS-PLATFORM: プラットフォーム連携

- [MASWE-0053](Document/weaknesses/MASVS-PLATFORM/MASWE-0053.md) ユーザーインタフェースから漏洩した機密データ (Sensitive Data Leaked via the User Interface)
- [MASWE-0054](Document/weaknesses/MASVS-PLATFORM/MASWE-0054.md) 通知から漏洩した機密データ (Sensitive Data Leaked via Notifications)
- [MASWE-0055](Document/weaknesses/MASVS-PLATFORM/MASWE-0055.md) スクリーンショットまたはスクリーン録画から漏洩した機密データ (Sensitive Data Leaked via Screenshots or Screen Recordings)
- [MASWE-0056](Document/weaknesses/MASVS-PLATFORM/MASWE-0056.md) タップジャッキング攻撃 (Tapjacking Attacks)
- [MASWE-0057](Document/weaknesses/MASVS-PLATFORM/MASWE-0057.md) StrandHogg 攻撃 / タスクアフィニティ脆弱性 (StrandHogg Attack / Task Affinity Vulnerability)
- [MASWE-0058](Document/weaknesses/MASVS-PLATFORM/MASWE-0058.md) 安全でないディープリンク (Insecure Deep Links)
- [MASWE-0059](Document/weaknesses/MASVS-PLATFORM/MASWE-0059.md) 認証されていないプラットフォーム IPC の使用 (Use Of Unauthenticated Platform IPC)
- [MASWE-0060](Document/weaknesses/MASVS-PLATFORM/MASWE-0060.md) UIActivity の安全でない使用 (Insecure Use of UIActivity)
- [MASWE-0061](Document/weaknesses/MASVS-PLATFORM/MASWE-0061.md) App Extension の安全でない使用 (Insecure Use of App Extensions)
- [MASWE-0062](Document/weaknesses/MASVS-PLATFORM/MASWE-0062.md) 安全でないサービス (Insecure Services)
- [MASWE-0063](Document/weaknesses/MASVS-PLATFORM/MASWE-0063.md) 安全でないブロードキャストレシーバ (Insecure Broadcast Receivers)
- [MASWE-0064](Document/weaknesses/MASVS-PLATFORM/MASWE-0064.md) 安全でないコンテンツプロバイダ (Insecure Content Providers)
- [MASWE-0065](Document/weaknesses/MASVS-PLATFORM/MASWE-0065.md) 他のアプリと永続的に共有される機密データ (Sensitive Data Permanently Shared with Other Apps)
- [MASWE-0066](Document/weaknesses/MASVS-PLATFORM/MASWE-0066.md) 安全でないインテント (Insecure Intents)
- [MASWE-0067](Document/weaknesses/MASVS-PLATFORM/MASWE-0067.md) 無効化されていないデバッグフラグ (Debuggable Flag Not Disabled)
- [MASWE-0068](Document/weaknesses/MASVS-PLATFORM/MASWE-0068.md) WebView での JavaScript ブリッジ (JavaScript Bridges in WebViews)
- [MASWE-0069](Document/weaknesses/MASVS-PLATFORM/MASWE-0069.md) ローカルリソースへのアクセスを許可する WebView (WebViews Allows Access to Local Resources)
- [MASWE-0070](Document/weaknesses/MASVS-PLATFORM/MASWE-0070.md) 信頼できないソースからロードされた JavaScript (JavaScript Loaded from Untrusted Sources)
- [MASWE-0071](Document/weaknesses/MASVS-PLATFORM/MASWE-0071.md) 信頼できないソースからコンテンツをロードする WebView (WebViews Loading Content from Untrusted Sources)
- [MASWE-0072](Document/weaknesses/MASVS-PLATFORM/MASWE-0072.md) ユニバーサル XSS (Universal XSS)
- [MASWE-0073](Document/weaknesses/MASVS-PLATFORM/MASWE-0073.md) 安全でない WebResourceResponse 実装 (Insecure WebResourceResponse Implementations)
- [MASWE-0074](Document/weaknesses/MASVS-PLATFORM/MASWE-0074.md) ウェブコンテンツのデバッグ有効化 (Web Content Debugging Enabled)

### MASVS-CODE: コード品質

- [MASWE-0075](Document/weaknesses/MASVS-CODE/MASWE-0075.md) 実装されていない強制アップデート (Enforced Updating Not Implemented)
- [MASWE-0076](Document/weaknesses/MASVS-CODE/MASWE-0076.md) 既知の脆弱性を持つ依存関係 (Dependencies with Known Vulnerabilities)
- [MASWE-0077](Document/weaknesses/MASVS-CODE/MASWE-0077.md) 確保されていない最新のプラットフォームバージョンでの実行 (Running on a recent Platform Version Not Ensured)
- [MASWE-0078](Document/weaknesses/MASVS-CODE/MASWE-0078.md) ターゲットになっていない最新プラットフォームバージョン (Latest Platform Version Not Targeted)
- [MASWE-0079](Document/weaknesses/MASVS-CODE/MASWE-0079.md) ネットワークからのデータの安全でない取り扱い (Unsafe Handling of Data from the Network)
- [MASWE-0080](Document/weaknesses/MASVS-CODE/MASWE-0080.md) バックアップからのデータの安全でない取り扱い (Unsafe Handling of Data from Backups)
- [MASWE-0081](Document/weaknesses/MASVS-CODE/MASWE-0081.md) 外部インタフェースからのデータの安全でない取り扱い (Unsafe Handling Of Data From External Interfaces)
- [MASWE-0082](Document/weaknesses/MASVS-CODE/MASWE-0082.md) ローカルストレージからのデータの安全でない取り扱い (Unsafe Handling of Data From Local Storage)
- [MASWE-0083](Document/weaknesses/MASVS-CODE/MASWE-0083.md) ユーザーインタフェースからのデータの安全でない取り扱い (Unsafe Handling of Data From The User Interface)
- [MASWE-0084](Document/weaknesses/MASVS-CODE/MASWE-0084.md) IPC からのデータの安全でない取り扱い (Unsafe Handling of Data from IPC)
- [MASWE-0085](Document/weaknesses/MASVS-CODE/MASWE-0085.md) 安全でない動的コードローディング (Unsafe Dynamic Code Loading)
- [MASWE-0086](Document/weaknesses/MASVS-CODE/MASWE-0086.md) SQL インジェクション (SQL Injection)
- [MASWE-0087](Document/weaknesses/MASVS-CODE/MASWE-0087.md) 安全でないパースとエスケープ (Insecure Parsing and Escaping)
- [MASWE-0088](Document/weaknesses/MASVS-CODE/MASWE-0088.md) 安全でないオブジェクトのデシリアライゼーション (Insecure Object Deserialization)
- [MASWE-0116](Document/weaknesses/MASVS-CODE/MASWE-0116.md) 使用されていないコンパイラ提供のセキュリティ機能 (Compiler Provided Security Features Not Used)

### MASVS-RESILIENCE: リバースエンジニアリングと改竄に対する耐性

- [MASWE-0008](Document/weaknesses/MASVS-RESILIENCE/MASWE-0008.md) デバイスのセキュアロック検証の実装の欠如 (Missing Device Secure Lock Verification Implementation)
- [MASWE-0089](Document/weaknesses/MASVS-RESILIENCE/MASWE-0089.md) 実装されていないコード難読化 (Code Obfuscation Not Implemented)
- [MASWE-0090](Document/weaknesses/MASVS-RESILIENCE/MASWE-0090.md) 実装されていないリソース難読化 (Resource Obfuscation Not Implemented)
- [MASWE-0091](Document/weaknesses/MASVS-RESILIENCE/MASWE-0091.md) 実装されていない逆難読化防止技法 (Anti-Deobfuscation Techniques Not Implemented)
- [MASWE-0092](Document/weaknesses/MASVS-RESILIENCE/MASWE-0092.md) 阻止されていない静的解析ツール (Static Analysis Tools Not Prevented)
- [MASWE-0093](Document/weaknesses/MASVS-RESILIENCE/MASWE-0093.md) 削除されていないデバッグシンボル (Debugging Symbols Not Removed)
- [MASWE-0094](Document/weaknesses/MASVS-RESILIENCE/MASWE-0094.md) 削除されていない非本番リソース (Non-Production Resources Not Removed)
- [MASWE-0095](Document/weaknesses/MASVS-RESILIENCE/MASWE-0095.md) 削除されていないセキュリティコントロールを無効にするコード (Code That Disables Security Controls Not Removed)
- [MASWE-0096](Document/weaknesses/MASVS-RESILIENCE/MASWE-0096.md) 暗号化された接続で暗号化されずに送信されるデータ (Data Sent Unencrypted Over Encrypted Connections)
- [MASWE-0097](Document/weaknesses/MASVS-RESILIENCE/MASWE-0097.md) 実装されていないルート/脱獄検出 (Root/Jailbreak Detection Not Implemented)
- [MASWE-0098](Document/weaknesses/MASVS-RESILIENCE/MASWE-0098.md) 実装されていないアプリ仮想化環境検出 (App Virtualization Environment Detection Not Implemented)
- [MASWE-0099](Document/weaknesses/MASVS-RESILIENCE/MASWE-0099.md) 実装されていないエミュレータ検出 (Emulator Detection Not Implemented)
- [MASWE-0100](Document/weaknesses/MASVS-RESILIENCE/MASWE-0100.md) 実装されていない Device Attestation (Device Attestation Not Implemented)
- [MASWE-0101](Document/weaknesses/MASVS-RESILIENCE/MASWE-0101.md) 実装されていないデバッガ検出 (Debugger Detection Not Implemented)
- [MASWE-0102](Document/weaknesses/MASVS-RESILIENCE/MASWE-0102.md) 実装されていない動的解析ツール検出 (Dynamic Analysis Tools Detection Not Implemented)
- [MASWE-0103](Document/weaknesses/MASVS-RESILIENCE/MASWE-0103.md) 実装されていない RASP 技法 (RASP Techniques Not Implemented)
- [MASWE-0104](Document/weaknesses/MASVS-RESILIENCE/MASWE-0104.md) 検証されていないアプリ完全性 (App Integrity Not Verified)
- [MASWE-0105](Document/weaknesses/MASVS-RESILIENCE/MASWE-0105.md) 検証されていないアプリリソースの完全性 (Integrity of App Resources Not Verified)
- [MASWE-0106](Document/weaknesses/MASVS-RESILIENCE/MASWE-0106.md) 実装されていない公式ストア検証 (Official Store Verification Not Implemented)
- [MASWE-0107](Document/weaknesses/MASVS-RESILIENCE/MASWE-0107.md) 検証されていないランタイムコード完全性 (Runtime Code Integrity Not Verified)

### MASVS-PRIVACY: プライバシー

- [MASWE-0108](Document/weaknesses/MASVS-RESILIENCE/MASWE-0108.md) ネットワークトラフィックの機密データ (Sensitive Data in Network Traffic)
- [MASWE-0109](Document/weaknesses/MASVS-RESILIENCE/MASWE-0109.md) 匿名化対策や仮名化対策の欠如 (Lack of Anonymization or Pseudonymisation Measures)
- [MASWE-0110](Document/weaknesses/MASVS-RESILIENCE/MASWE-0110.md) ユーザー追跡のための固有識別子の使用 (Use of Unique Identifiers for User Tracking)
- [MASWE-0111](Document/weaknesses/MASVS-RESILIENCE/MASWE-0111.md) 不十分なプライバシーポリシー (Inadequate Privacy Policy)
- [MASWE-0112](Document/weaknesses/MASVS-RESILIENCE/MASWE-0112.md) 不十分なデータ収集宣言 (Inadequate Data Collection Declarations)
- [MASWE-0113](Document/weaknesses/MASVS-RESILIENCE/MASWE-0113.md) 適切なデータ管理コントロールの欠如 (Lack of Proper Data Management Controls)
- [MASWE-0114](Document/weaknesses/MASVS-RESILIENCE/MASWE-0114.md) 不十分なデータ可視性コントロール (Inadequate Data Visibility Controls)
- [MASWE-0115](Document/weaknesses/MASVS-RESILIENCE/MASWE-0115.md) 不十分または曖昧なユーザー同意メカニズム (Inadequate or Ambiguous User Consent Mechanisms)
- [MASWE-0117](Document/weaknesses/MASVS-RESILIENCE/MASWE-0117.md) 不十分なパーミッション管理 (Inadequate Permission Management)

## License

[Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/)

## Translator (Japanese)

[Koki Takeyama](https://github.com/coky-t)

- Document Site - <https://coky-t.gitbook.io/owasp-docs-ja/>
- Document Repository - <https://github.com/coky-t/owasp-docs-ja>
