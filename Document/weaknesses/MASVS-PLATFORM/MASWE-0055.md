---
title: スクリーンショットまたはスクリーン録画から漏洩した機密データ (Sensitive Data Leaked via Screenshots or Screen Recordings)
id: MASWE-0055
alias: data-leak-screenshots
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-STORAGE-9]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]

refs:
- https://developer.android.com/about/versions/14/features/screenshot-detection
status: new

---

## 概要

モバイルプラットフォームでは、ユーザーやサードパーティのツールがスクリーンショットをキャプチャしたり、スクリーンを録画できます。これは機密データをさらし、データ漏洩のリスクを高める可能性があります。

攻撃者がこの機密データを入手する方法はいくつかあります。

- **スクリーンのキャプチャまたは録画するためのパーミッションを持つサードパーティアプリ**: サードパーティアプリは機密コンテンツが表示されている際にスクリーンを録画する可能性があります。
- **スクリーンショットおよび録画ファイルにアクセスするためのパーミッションを持つサードパーティアプリ**: サードパーティアプリは、ユーザーまたはツールによって取得された後、ストレージに保存されたスクリーンショットや録画にアクセスする可能性があります。
- **外部ツールによるスクリーン録画の可能性**: [Scrcpy](https://github.com/coky-t/owasp-mastg-ja/blob/master/tools/android/MASTG-TOOL-0024.md) や [libimobiledevice suite](https://github.com/coky-t/owasp-mastg-ja/blob/master/tools/ios/MASTG-TOOL-0126.md) などのツールは USB 接続を介してデバイスのスクリーンを録画できます。
- **バックグラウンド移行時の自動スクリーンショット**: アプリがバックグラウンド状態に入ると、システムはアプリの現在のビューのスクリーンショットをキャプチャし、アプリスイッチャーに表示する可能性があります。これらのスクリーンショットはファイルシステムに保存され、悪意のある人物によってアクセスされたり盗まれる可能性があります。

## 影響

- **Loss of Confidentiality**: Under certain conditions, an attacker could access sensitive data previously displayed on the screen, potentially compromising confidentiality and enabling further attacks, such as identity theft or account takeover.

## 流入の形態

This can typically occur in two ways:

- **Screenshots and Screen Recordings Not Prevented:** The app does not implement measures (such as setting secure window flags) to prevent the operating system or other apps from capturing screenshots or screen recordings.
- **Unredacted Sensitive On-Screen Content:** The app displays sensitive information directly on the screen without masking or redacting it, allowing confidential data to be visible if a screenshot or screen recording is taken.

## 緩和策

- Prevent screenshots and screen recording.
- Redact sensitive on-screen content so that, if a screenshot is taken, no confidential data is visible.
