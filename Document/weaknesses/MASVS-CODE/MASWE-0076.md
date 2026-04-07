---
title: 既知の脆弱性を持つ依存関係 (Dependencies with Known Vulnerabilities)
id: MASWE-0076
alias: dependencies-with-known-vulnerabilities
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CODE-5]
  masvs-v2: [MASVS-CODE-3]
  cwe: [1395, 1357]
  android-core-app-quality: [SC-N3, PS-T4]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/insecure-library
  nist-ssdf: [PS.3.2]
status: new
refs:
- https://developer.android.com/privacy-and-security/risks/insecure-library
- https://www.cisa.gov/sites/default/files/2023-04/sbom-types-document-508c.pdf
- https://www.ntia.doc.gov/files/ntia/publications/sbom_minimum_elements_report.pdf
- https://developer.android.com/guide/practices/sdk-best-practices
- https://developer.android.com/privacy-and-security/security-best-practices#services-dependencies-updated
- https://developer.android.com/privacy-and-security/security-best-practices#update-dependencies
- https://support.google.com/googleplay/android-developer/answer/14514531
- https://support.google.com/googleplay/android-developer/answer/13326895
- https://developer.apple.com/support/third-party-SDK-requirements/
- https://www.youtube.com/watch?v=3klmiHX0uVQ
- https://developer.apple.com/videos/play/wwdc2023/10060/
---

## 概要

モバイルアプリは、機能の実装、開発の効率化、プラットフォームサービスの統合のために、コミュニティによって保守されているオープンソースコンポーネントまたは商用ベンダーによって提供されるクローズドソース製品のいずれかの、サードパーティライブラリ、ソフトウェア開発キット (SDK)、フレームワークに依存することがよくあります。

これらの依存関係に脆弱性を含む場合、これらの脆弱性 (および一部のエクスプロイト) は CVE リストなどの公開データベースに文書化されていたり、セキュリティアドバイザリを通じてアクセス可能であることが多いため、ファーストパーティコードの脆弱性よりも簡単に悪用される可能性があります。

**開発者は** すべての依存関係が安全かつ最新であることを確保する **責任があります**。なぜなら、それらはアプリのコードベースの一部であり、それゆえにアプリの攻撃対象領域を拡大するためです。Google と Apple は以下のセキュリティベストプラクティスでこれを強調しています。

> [!NOTE]
> "Google の [Using SDKs safely and securely](https://support.google.com/googleplay/android-developer/answer/13326895)"  
> "アプリに SDK を含む場合、サードパーティのコードとプラクティスが Google Play Developer Program Policies に準拠していること、およびアプリがポリシーに違反しないことを確保する責任があなたにあります。"

> [!NOTE]
> "Apple の [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)"  
> "広告ネットワーク、分析サービス、サードパーティ SDK など、アプリ内のすべてがこれらのガイドラインに準拠していることを確認するのはあなたの責任ですので、慎重に確認して選択してください。"

プライバシーの観点では、依存関係が適切な同意や透明性なしにユーザーデータを収集したり送信する場合、リスクをもたらす可能性があります。Google と Apple の両社は、アプリで使用されるサードパーティ SDK に、ユーザーデータが安全かつ透明性のあるように取り扱われることを確保するため、それぞれのプライバシーポリシーとガイドラインを遵守することを求めています。たとえライブラリ自体が直接管理下にない場合や、プラットフォームのポリシーに違反する可能性のある特定のコードを使用していない場合でも、アプリで使用されるサードパーティライブラリや SDK がこれらの要件に遵守していることを確保するのは開発者の責任です。

> [!NOTE]
> "Google の [Using SDKs safely and securely](https://support.google.com/googleplay/android-developer/answer/13326895)"  
> "アプリ開発者は、SDK によってアプリ内で収集されたデータを、直接収集したかのように扱う必要があります。"

> [!NOTE]
> "Apple の [Third-party SDK requirements](https://developer.apple.com/support/third-party-SDK-requirements/)"  
> "アプリでサードパーティ SDK を使用する場合、SDK がアプリに含めるすべてのコードについてあなたが責任を負い、そのデータ収集や使用方法を把握する必要があります。"

プライバシーとデータ収集に関する宣言の詳細については、[不十分なデータ収集宣言 (Inadequate Data Collection Declarations)](../MASVS-PRIVACY/MASWE-0112.md) を参照してください。

## 影響

モバイルアプリで既知の脆弱性を持つ依存関係を使用すると、以下のようなさまざまなセキュリティリスクにつながる可能性があります。ただし、これらに限定されません。

- **機密データの露出**: 脆弱な依存関係は悪用され、アクセス制御や暗号化保護をバイパスする可能性があり、クレデンシャル、セッショントークン、個人を識別できる情報 (PII) などの機密性の高いユーザーデータの露出につながる可能性があります。これはデータ侵害につながり、法的、経済的、評判的な悪影響を及ぼす可能性があります。
- **不正なコードの実行や権限昇格**: 組み込まれた依存関係の悪用可能な脆弱性は、攻撃者がアプリのコンテキスト内で (例: コードインジェクションを通じて) 任意のコードを実行したり、権限を昇格したり、アプリの動作を操作することを可能性にします。全体的な影響は、ユーザーアカウントの完全な侵害、バックエンドサービスの悪用、保護されたリソースへの永続的なアクセスなど多岐にわたります。ビジネスへの影響は深刻で、金銭的損失、サービス中断、顧客からの信頼の失墜などを含みます。
- **規制およびポリシーの非遵守**: 公知の CVE を持つ依存関係を含むと、規制要件 (GDPR, HIPAA, PCI-DSS など) やプラットフォームセキュリティポリシー (Google Play や App Store のガイドラインなど) に違反する可能性があります。このような脆弱性を更新または修正しないと、アプリの不認可、罰金、開示義務につながる可能性があります。

## 流入の形態

- **直接的な依存関係**: 脆弱な依存関係は、手動で (ソースファイルやバイナリファイルをコピーしてリンクすることで) アプリにもたらされることもあれば、より一般的にはパッケージマネージャやビルドツール (Gradle, CocoaPods, Swift Package Manager など) を介してもたらされることもあります。これはファーストパーティおよびサードパーティの SDK を含み、静的および動的にリンクする両方のライブラリが関与する可能性があります。
- **推移的依存関係**: 依存関係はアプリが使用する他のライブラリや SDK を通じて間接的に取り込まれることがあります。つまり、アプリが脆弱なライブラリ自体を直接含んでいなくても、依存関係のいずれかがそれを含む場合、アプリは依然としてその影響を受ける可能性があることを意味します。
- **動的にロードされる依存関係**: 一部のライブラリは実行時に動的にロードされることがあり、依存関係の追跡と管理を困難にする可能性があります。これは、開発者の知らないうちに脆弱なバージョンのライブラリが使用される事態につながる可能性があります。
- **古くなったプラットフォームセキュリティコンポーネント**: モバイルアプリは、暗号ライブラリや SSL/TLS 実装など、プラットフォームが提供するセキュリティコンポーネントに依存していることがあります。これらのコンポーネントが古くなっていたり、タイムリーな更新を欠いている場合、既知の脆弱性をアプリケーションにもたらす可能性があります。たとえば、Android では、安全なネットワーク通信を担うシステムのセキュリティプロバイダは、アプリ起動時に開発者によって明示的に更新される必要があります。
- **サードパーティフレームワークの使用**: アプリケーションは Flutter や React Native などのサードパーティアプリケーションフレームワークで構築されることがあります。フレームワーク自体、およびプラットフォーム固有のバインディングには脆弱性を含む可能性があります。

## 緩和策

- **Use a Software Bill of Materials (SBOM)**: Produce and maintain an SBOM to track all components and transitive dependencies, ensuring visibility and accountability for third-party code. See [NIST SSDF (NIST SP 800-218) PS.3.2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-218.pdf), [NTIA The Minimum Elements For a Software Bill of Materials (SBOM)](https://www.ntia.doc.gov/files/ntia/publications/sbom_minimum_elements_report.pdf), [CISA SBOM Types document](https://www.cisa.gov/sites/default/files/2023-04/sbom-types-document-508c.pdf) for more information on SBOMs and their importance in managing software dependencies.
- **Update Dependencies Responsibly**: As part of secure [dependency management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html), regularly monitor all used third-party dependencies for security-related updates (for example, by using Software Composition Analysis (SCA) tools and SBOMs in your CI/CD pipelines). Apply updates when they fix known vulnerabilities, and pin versions explicitly to prevent unexpected changes and reduce the risk of supply-chain attacks.
- **Remove Unused or Obsolete Dependencies**: Periodically review and eliminate unused, legacy, or unnecessary libraries to reduce the app's attack surface and dependency footprint.
- **Use Trusted Sources**: Only include libraries and SDKs from reputable sources, such as official repositories or well-maintained open-source projects, to minimize the risk of introducing malicious or vulnerable code.
