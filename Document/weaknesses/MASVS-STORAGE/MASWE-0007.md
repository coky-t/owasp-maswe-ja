---
title: ユーザーの介入を必要としない共有ストレージに暗号化されずに保存される機密データ (Sensitive Data Stored Unencrypted in Shared Storage Requiring No User Interaction)
id: MASWE-0007
alias: data-unencrypted-shared-storage-no-user-interaction
platform: [android]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-STORAGE-2]
  masvs-v2: [MASVS-STORAGE-1]
  mastg-v1: [MASTG-TEST-0052, MASTG-TEST-0001]
  cwe: [312, 313, 921, 922]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/sensitive-data-external-storage
status: new
---

## 概要

アプリは、容量が大きいために、外部ストレージにデータを保存することを選択することがよくあります。しかし、この利便性には潜在的なセキュリティ上の欠点を伴います。悪意のあるアプリが重要なパーミッションを付与されると、ユーザーの同意ややり取りなしにいつでもこのデータにアクセスできます。さらに、SD カードなどの外部ストレージは、悪意のある人物により物理的に取り外され、読み取られる可能性があります。たとえ外部ストレージがシステムによってエミュレートされていたとしても、不適切なファイルパーミッションやファイル保存用の API の誤用によってリスクが生じます。そのような場合、ファイルは不正アクセス、改変、削除に対して脆弱になり、アプリケーションにとってセキュリティ脅威となります。

開発者は、より高いプライバシーとセキュリティを必要とする場合、プライベートストレージやユーザーインタラクションを必要とする共有ストレージへの切り替えを検討できます。しかし、外部ストレージがアプリにとって最適である場合には、外部ストレージに保存するデータを暗号化することをお勧めします。以下では、外部ストレージの使用に関連する潜在的なセキュリティへの影響と緩和策を見出します。

## 影響

- **Loss of confidentiality**: An attacker can extract sensitive data stored externally, such as personal information and media like photos, documents, and audio files.

- **Loss of secure material**: An attacker can extract passwords, cryptographic keys, and session tokens to facilitate additional attacks, such as identity theft or account takeover.

- **Modification of app's behaviour**: An attacker can tamper with data used by the app, altering the app's logic. For example, they could modify a database describing the state of premium features or inject a malicious payload to enable further attacks such as SQL injection and Path Traversal.

- **Modification of downloaded code**: An app can download new functionality from the Internet and store the executable code in external storage before loading it into the process. An attacker can modify this code before it is used by the app.

## 流入の形態

This threat is primarily a concern for Android devices since they permit the use of external storage. Even if a device lacks physical external storage, Android emulates it to provide access to the external storage API.

- **Data Stored Unencrypted**: Sensitive data is stored in the external storage unencrypted.
- **Hardcoded Encryption Key**: Sensitive data is encrypted and stored in the external storage but the key is hardcoded inside the application.
- **Encryption Key Stored on Filesystem**: Sensitive data is encrypted and stored in the external storage but the key is stored alongside it or in another easily accessible location.
- **Encryption Used is Insufficient**: Sensitive data is encrypted but the encryption is not considered to be strong.
- **Reuse of encryption key**: The encryption key is shared between two devices owned by a single user, enabling the process of data cloning between these devices in the external storage.

On iOS, apps cannot directly write to or read from the arbitrary locations, as compared to desktop operating system or Android. iOS maintains strict sandboxing rules, meaning apps can only access their own sandboxed file directories.

## 緩和策

Sensitive data stored in the external storage should be encrypted, and any keys used for data encryption should be protected by the device's hardware-backed keystore, where available. It is highly discouraged to include cryptographic keys hardcoded inside the application. You can also consider storing your files in the [private app sandbox or internal storage](https://developer.android.com/training/data-storage/app-specific#internal) and using [Android's EncryptedFile API wrapper for file encryption](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile).

!!! Warning

    The **Jetpack security crypto library**, including the `EncryptedFile` and  `EncryptedSharedPreferences` classes, has been [deprecated](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library). However, since an official replacement has not yet been released, we recommend using these classes until one is available.
