---
title: ユーザー追跡のための固有識別子の使用 (Use of Unique Identifiers for User Tracking)
id: MASWE-0110
alias: unique-identifiers-user-tracking
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-2]
  cwe: [359]
refs:
- https://developer.android.com/reference/android/provider/Settings.Secure#ANDROID_ID
- https://developer.android.com/privacy-and-security/about#resettable-identifiers
- https://developer.android.com/identity/user-data-ids
- https://developer.android.com/identity/user-data-ids#common-use-cases
- https://developer.android.com/identity/ad-id
- https://developers.google.com/privacy-sandbox/private-advertising/attribution-reporting/android
- https://developer.apple.com/app-store/app-privacy-details/#user-tracking
- https://developer.apple.com/app-store/user-privacy-and-data-use/
- https://developer.apple.com/documentation/apptrackingtransparency/
- https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier
- https://developer.apple.com/documentation/uikit/uidevice/1620059-identifierforvendor/
- https://developer.apple.com/app-store/ad-attribution/
- https://developer.apple.com/documentation/adattributionkit
- https://gdpr-info.eu/recitals/no-30/

status: new
---

## 概要

モバイルアプリケーションでのユーザー追跡は、ユーザーの行動、嗜好、活動を監視するためのデータ収集と解析を伴います。これは企業が時間の経過とともにさまざまなアプリ、デバイス、サービスにわたってユーザーを認識して追跡できます。そのような追跡はユーザーの明示的な認識や同意なしに発生することが多く、重大なプライバシー上の懸念につながります。

モバイルアプリは、Google, Meta (旧 Facebook), X (旧 Twitter) などの企業からのユーティリティやサードパーティ SDK を組み込まれることがよくあります。これらのユーティリティの例としては、分析ツール、広告ネットワーク、ソーシャルメディア統合コンポーネントなどがあります。これらのコンポーネントはアプリの機能に直接関係のないデータを収集する可能性があり、付与されたパーミッションによっては、連絡先リストや位置情報履歴などの機密情報にアクセスする可能性があります。デバイス製造業者がプリインストールしたアプリは、ユーザーの知らないうちに侵襲的なデータ収集を行う可能性があるため、問題をさらに複雑にする可能性があります。

追跡のよくある手法の一つは固有識別子、特にリセットできないもの、を使用することです。複数のアプリからのデータと組み合わせることで、これらの識別子を使用して個人の詳細なプロファイルを作成し、興味、健康状態、性的指向、その他の個人属性を推定できます。この情報は、ターゲット広告、パーソナライズされたコンテンツ配信、さらには政治的意見に影響を与えるために活用される可能性があります。

## 流入の形態

- **リセット不可能な識別子の使用**: デバイス ID、ハードウェアシリアル番号、MAC アドレスなど、ユーザーがリセットできない識別子を利用すると、ユーザーの同意なしに永続的な追跡につながる可能性があります。たとえば、Android 8.0 (API レベル 26) 以前の [ANDROID_ID](https://developer.android.com/reference/android/provider/Settings.Secure#ANDROID_ID) は初回起動時にランダムに生成されるリセット不可能な識別子でしたが、最近のバージョンでは、アプリ署名鍵、ユーザー、デバイスの組み合わせごとに一意になっています。
- **リセット可能な識別子の不正使用**: Android の [広告 ID](https://developer.android.com/identity/user-data-ids#advertising-ids) や iOS の [広告識別子 (別名: 広告主向け識別子または IDFA)](https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier) などの [リセット可能な識別子](https://developer.android.com/privacy-and-security/about#resettable-identifiers) を、ユーザーの設定を尊重したり適切な同意を得たりせずに使用すると、不正な追跡につながる可能性があります。
- **サービス間での識別子のリンク**: 異なるサービスやアプリ間で識別子をリンクすることで、リセットや再インストール後でも、ユーザーの統一されたプロファイルを作成できます。これは、デバイス ID、広告 ID、その他の固有識別子、行動データなど、さまざまなソースからの識別子を組み合わせることで実現できます。
- **ユーザーの同意なしでの追跡**: 明示的な同意なしに、またはオプトアウトや識別子のリセット機能を提供せずに、サービスやアプリ間でユーザーを追跡します。たとえば、iOS では [App Tracking Transparency (ATT) フレームワーク](https://developer.apple.com/documentation/AppTrackingTransparency) の下で、IDFA へのアクセスには明示的な同意を要求します。IDFV は明示的な同意なしに同じベンダーのアプリ間でユーザーを追跡できますが、そのベンダーのすべてのアプリがデバイスから削除されるとリセットします。

## 影響

- **ユーザーの信頼の喪失**: 追跡に固有の識別子がどのように使用されるかについて透明性が欠如しているアプリでは、ユーザーは信頼を失う可能性が高く、否定的なレビュー、エンゲージメントの低下、維持率の低下につながる可能性があります。
- **ユーザープライバシーの侵害**: ユーザーは、固有の識別子や使用パターンの収集といった、追跡を受け入れる際の影響を十分に認識していない可能性があります。場合によっては、アプリの使用に追跡が必須となり、ユーザーに実質的な選択肢がないこともあります。これは、プライバシー侵害、情報の不正使用、ユーザーのデータ管理の侵害につながる可能性があります。
- **コンプライアンスおよび法的リスク**: データ保護法や規制 (GDPR など) の違反は、法的措置や罰金をもたらし、プラットフォームガイドラインに準拠しない可能性があり、アプリストアからの削除につながる可能性があります。

## 緩和策

- **リセット可能な識別子を使用する**: 分析やパーソナライズ広告などの目的では、Android の [広告 ID](https://developer.android.com/identity/user-data-ids#advertising-ids) や iOS の [広告識別子 (別名: 広告主向け識別子または IDFA)](https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier) などの [リセット可能な識別子](https://developer.android.com/privacy-and-security/about#resettable-identifiers) を優先します。追跡とデータ収集に関してはユーザーの設定と同意を常に尊重します。デバイス ID や MAC アドレスなどのハードウェアベースの識別子の使用は避けます。
- **アプリスコープの識別子を使用する**: アプリスコープの識別子を使用して、ユーザープライバシーを維持し、サービス間の追跡を防止します。例としては [**ANDROID_ID** (Android 8.0 (API レベル 26) 以降)](https://developer.android.com/about/versions/oreo/android-8.0-changes#privacy-all), **Firebase インストール ID (FID)**, 非公開で保存されたグローバル一意識別子 (GUID) などがあります。iOS では、**ベンダー識別子 (IDFV)** を使用して、同じベンダーのアプリ間でユーザーを追跡し、そのベンダーのアプリがすべてアンインストールされた際にリセットすることを検討します。
- **広告 ID を適切に使用する**: 広告 ID の使用は広告配信とユーザープロファイリングのコンテキストに限定し、広告トラッキングに関するユーザー設定を尊重します。リセット後に明示的なユーザー同意なしに識別子をリンクすることは避け、改めてやり直すようにします。Android では、[**広告 ID** を適切に使用する](https://support.google.com/googleplay/android-developer/answer/9857753#ad-id)、iOS では、**広告主向け識別子 (Identifier for Advertisers, IDFA)** にアクセスする前に [ユーザーに許可を求める](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/requesttrackingauthorization(completionhandler:)) ことで **App Tracking Transparency (ATT)** に準拠し、それを保存することは避けます。代わりに [`advertisingIdentifier`](https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier) にアクセスします。
- **適切な API を使用する**: 識別子に頼るのではなく、プライバシーを保護する API を使用します。たとえば、Android でのデバイス検証は **Play Integrity** を使用し、iOS では **DeviceCheck** を使用します (プロモーションオファーを活用するデバイスを識別したり、不正なデバイスをフラグ付けするためなど)。プライバシーに配慮した広告アトリビューションには、Android では [Attribution Reporting API](https://developers.google.com/privacy-sandbox/private-advertising/attribution-reporting/android) を使用し、iOS では **AdAttributionKit** または **SKAdNetwork** を使用することを検討します。
- **サードパーティ SDK を独自のコードとして扱う**: アプリに統合されているサードパーティ SDK に関連するプライバシーまたはセキュリティポリシー、特に固有識別子の使用に関するものに注意します。識別子の不正使用を避け、透明性を確保するために、サードパーティ SDK が、Apple の App Tracking Transparency (ATT) や Google の Play Data Safety ポリシーなど、データ収集とユーザー同意に関するプラットフォームガイドラインに準拠していることを確保します。
- **明確なプライバシー情報を提供する**: プライバシーポリシー、アプリストアの掲載情報、およびアプリ自体の中で、固有識別子の収集と使用についてユーザーに通知します。追跡の目的と、それがユーザーエクスペリエンスにどのような恩恵をもたらすかを明確に説明します。可能であれば、ユーザーが追跡をオプトアウトしたり、識別子をリセットできるようにします。
