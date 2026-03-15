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

Using dependencies with known vulnerabilities in mobile apps can result in various security risks, including but not limited to:

- **Sensitive Data Exposure**: Vulnerable dependencies may be exploited to bypass access controls or cryptographic protections, which could lead to the exposure of sensitive user data, including credentials, session tokens, and personally identifiable information (PII). This can result in data breaches, which can have legal, financial and reputational consequences.
- **Execution of Unauthorized Code or Privilege Escalation**: Exploitable vulnerabilities in embedded dependencies can allow attackers to execute arbitrary code within the app's context (e.g., through code injection), escalate privileges, or manipulate app behavior. The overall impact can range from full compromise of user accounts, abuse of backend services or persistent access to protected resources. The business impact can be severe, including financial loss, service disruption, and damage to customer trust.
- **Regulatory and Policy Non-Compliance**: Including dependencies with publicly known CVEs may violate regulatory requirements (e.g., GDPR, HIPAA, PCI-DSS) or platform security policies (e.g., Google Play or App Store guidelines). Failure to update or remediate such vulnerabilities can result in app rejection, fines, or mandatory disclosures.

## 流入の形態

- **Direct Dependencies**: Vulnerable dependencies can be introduced into the app either manually (by copying and linking source or binary files) or more commonly via package managers and build tools (e.g., Gradle, CocoaPods, Swift Package Manager). This includes both first- and third-party SDKs, and may involve both statically and dynamically linked libraries.
- **Transitive Dependencies**: Dependencies can be pulled in indirectly through other libraries or SDKs that the app uses. This means that an app may still be affected by a vulnerable library if one of its dependencies includes it, even if the app does not directly include the library itself.
- **Dynamically Loaded Dependencies**: Some libraries may be dynamically loaded at runtime, which can make it difficult to track and manage dependencies. This can lead to situations where a vulnerable version of a library is used without the developer's knowledge.
- **Outdated Platform Security Components**: Mobile apps may depend on platform-provided security components, such as cryptographic libraries or SSL/TLS implementations. If these components are outdated or lack timely updates, they can introduce known vulnerabilities into the application. For instance, on Android, the system's security provider responsible for secure network communications must be explicitly updated by the developer at app startup.
- **Usage of Third-Party Frameworks**: Applications may be built in a third-party application framework such as Flutter or React Native. The framework itself, as well as any platform-specific bindings may contain vulnerabilities.

## 緩和策

- **Use a Software Bill of Materials (SBOM)**: Produce and maintain an SBOM to track all components and transitive dependencies, ensuring visibility and accountability for third-party code. See [NIST SSDF (NIST SP 800-218) PS.3.2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-218.pdf), [NTIA The Minimum Elements For a Software Bill of Materials (SBOM)](https://www.ntia.doc.gov/files/ntia/publications/sbom_minimum_elements_report.pdf), [CISA SBOM Types document](https://www.cisa.gov/sites/default/files/2023-04/sbom-types-document-508c.pdf) for more information on SBOMs and their importance in managing software dependencies.
- **Update Dependencies Responsibly**: As part of secure [dependency management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html), regularly monitor all used third-party dependencies for security-related updates (for example, by using Software Composition Analysis (SCA) tools and SBOMs in your CI/CD pipelines). Apply updates when they fix known vulnerabilities, and pin versions explicitly to prevent unexpected changes and reduce the risk of supply-chain attacks.
- **Remove Unused or Obsolete Dependencies**: Periodically review and eliminate unused, legacy, or unnecessary libraries to reduce the app's attack surface and dependency footprint.
- **Use Trusted Sources**: Only include libraries and SDKs from reputable sources, such as official repositories or well-maintained open-source projects, to minimize the risk of introducing malicious or vulnerable code.
