---
title: 使用されていない実証済みネットワーク API (Proven Networking APIs Not used)
id: MASWE-0049
alias: no-proven-net-apis
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-NETWORK-6]
  masvs-v2: [MASVS-NETWORK-1, MASVS-CODE-3]
status: new
---

## 概要

プラットフォームが提供するネットワーク API や十分に確立されたセキュリティライブラリを利用しないアプリケーションはセキュリティ脆弱性の影響を受けやすくなります。開発者がカスタムネットワークコードや「独自 (roll-your-own)」のセキュリティメカニズムを実装すると、暗号技術やネットワークセキュリティに関する深い専門知識の不足により欠陥をもたらすリスクがあります。iOS の `NSURLSession` や Android の `HttpsURLConnection` などのプラットフォームが提供する API や ライブラリは専門家によって設計され保守されており、セキュリティのベストプラクティスを取り入れ、新たな脅威や脆弱性に対処するために定期的な更新を行っています。

## 影響

- **セキュリティの脆弱性**: カスタムネットワーク実装は攻撃者が悪用できる欠陥を含む可能性があり、データ侵害や不正アクセスにつながる可能性があります。
- **アップデートの欠如**: カスタムコードは、新たな脆弱性に対処したり、進化するセキュリティ標準に準拠するためのアップデートをタイムリーに受けられない可能性があります。
- **一貫性のないセキュリティ対策**: 標準 API をバイパスすると、暗号化、証明書バリデーション、エラー処理などのセキュリティ機能が一貫して適用されなくなる可能性があります。
- **開発の複雑さの増大**: カスタムネットワークコードの作成と保守は複雑さを増し、アプリケーションの監査と保護がより困難になります。
- **標準への非準拠**: 承認された API を使用しないと、業界の規制やセキュリティガイドラインへの非準拠につながる可能性があります。

## 流入の形態

- **カスタムネットワークスタックの開発**: 開発者は、カスタム機能を追加するため、または既存の API に慣れていないなどにより、プラットフォームが提供する API を使用する代わりに独自のネットワークコードを作成します。
- **安全でないサードパーティライブラリの使用**: 古くなった、あるいは現在のセキュリティベストプラクティスに従っていないサードパーティネットワークライブラリを組み込んでいます。
- **セキュリティメカニズムのバイパス**: 証明書のピン留めや TLS の強制などのセキュリティチェックを回避するために、標準 API を意図的に避けています。
- **不十分なセキュリティ知識**: 開発者はネットワークセキュリティの原則を十分に理解していないため、安全でない実装につながる可能性があります。
- **パフォーマンス最適化の試み**: セキュリティの影響を十分に考慮せずに、パフォーマンスを最適化するためにカスタムネットワークコードを記述しています。

## 緩和策

- **Utilize Platform-Provided Networking APIs**: Always use the networking APIs provided by the platform, such as `NSURLSession` for iOS and `HttpsURLConnection` for Android, which handle many security concerns internally.
- **Adopt Established Security Libraries**: If additional functionality is required, use reputable, well-maintained libraries like `OkHttp` for Android or `Alamofire` on iOS that adhere to security best practices.
- **Avoid Custom Security Implementations**: Refrain from implementing custom cryptographic algorithms or security protocols; rely on standard, vetted solutions instead.
- **Keep Dependencies Updated**: Regularly update all libraries and dependencies to incorporate the latest security patches and improvements.
