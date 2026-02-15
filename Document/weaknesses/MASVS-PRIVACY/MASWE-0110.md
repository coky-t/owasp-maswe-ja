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

- **Loss of User Trust**: Users are likely to lose trust in an app that lacks transparency in how unique identifiers are used for tracking, which may lead to negative reviews, decreased engagement, and reduced retention rates.
- **Violation of User Privacy**: Users may not be fully aware of the implications when accepting tracking, such as the collection of unique identifiers or usage patterns. In some cases, tracking may be mandatory to use an app, leaving users without a real choice. This can lead to privacy violations, unauthorized use of their information, and an erosion of user control over their data.
- **Compliance and Legal Risks**: Violation of data protection laws and regulations (like GDPR), resulting in legal consequences, fines, and potential non-compliance with platform guidelines, which may lead to app store removal.

## 緩和策

- **Use Resettable Identifiers**: Prefer [resettable identifiers](https://developer.android.com/privacy-and-security/about#resettable-identifiers) like the [Advertising ID](https://developer.android.com/identity/user-data-ids#advertising-ids) on Android or [Advertising Identifier (aka. Identifier for Advertiseers or IDFA)](https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier) on iOS, for purposes like analytics or personalized advertising. Always respect user preferences and consent regarding tracking and data collection. Avoid using hardware-based identifiers like device IDs or MAC addresses.
- **Use App-Scoped Identifiers**: Use app-scoped identifiers to maintain user privacy and prevent cross-service tracking. Examples include [**ANDROID_ID** (on Android 8.0 (API level 26) and higher)](https://developer.android.com/about/versions/oreo/android-8.0-changes#privacy-all), **Firebase Installation IDs (FIDs)**, or privately stored Globally Unique IDs (GUIDs). On iOS, consider using **Identifier for Vendors (IDFV)** to track users across apps by the same vendor and resets when all the vendor's apps are uninstalled.
- **Use Advertising ID Appropriately**: Restrict advertising ID usage to ad-serving and user profiling contexts, respecting user preferences on ad tracking. Avoid linking identifiers after a reset without explicit user consent, ensuring a fresh start. On Android, [use the **Advertising ID** appropriately](https://support.google.com/googleplay/android-developer/answer/9857753#ad-id), and on iOS, comply with **App Tracking Transparency (ATT)** by [requesting user permission](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/requesttrackingauthorization(completionhandler:)) before accessing the **Identifier for Advertisers (IDFA)** and avoid storing it; access [`advertisingIdentifier`](https://developer.apple.com/documentation/adsupport/asidentifiermanager/advertisingidentifier) instead.
- **Use Appropriate APIs**: Use privacy-preserving APIs instead of relying on identifiers. For example, for device verification on Android use **Play Integrity**, and on iOS use **DeviceCheck** (e.g., to identify devices that have taken advantage of a promotional offer or to flag fraudulent devices). For privacy-friendly ad attribution, use [Attribution Reporting API](https://developers.google.com/privacy-sandbox/private-advertising/attribution-reporting/android) on Android, and consider using **AdAttributionKit** or **SKAdNetwork** on iOS.
- **Treat Third-Party SDKs as Your Own Code**: Be aware of any privacy or security policies associated with third-party SDKs integrated into your app, particularly those related to the use of unique identifiers. Ensure third-party SDKs comply with platform guidelines for data collection and user consent, such as Apple's App Tracking Transparency (ATT) and Google's Play Data Safety policies, to avoid misuse of identifiers and ensure transparency.
- **Provide Clear Privacy Information**: Inform users about the collection and use of unique identifiers in your privacy policy, app store listing, and within the app itself. Clearly explain the purpose of tracking and how it benefits the user experience. Provide users with the ability to opt out of tracking or reset identifiers if possible.
