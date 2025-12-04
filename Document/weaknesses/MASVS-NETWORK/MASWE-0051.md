---
title: 保護されていないオープンポート (Unprotected Open Ports)
id: MASWE-0051
alias: open-ports
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-NETWORK-2]
  masvs-v2: [MASVS-NETWORK-1]
  cwe: [923]
status: new
---

## 概要

適切な保護なしでネットワークポートを開くアプリケーションは、不正アクセスや潜在的な悪用に脆弱です。この弱点は、アプリケーションがネットワークポートをリッスンし、適切なセキュリティ対策なしで着信接続を受け入れることで発生し、他のアプリケーションや攻撃者が接続してやり取りできるようになります。

## 影響

- **不正アクセス**: 攻撃者はオープンポートに接続し、アプリケーション機能や機密データにアクセスする可能性があります。
- **データ漏洩**: 適切な認証と暗号化が実施されていない場合、保護されていないポートを通じて機密情報がさらされる可能性があります。
- **リモートコード実行**: オープンポートの悪用によりデバイス上で任意のコードの実行につながる可能性があります。
- **サービス拒否**: 攻撃者はオープンポートに過負荷をかけ、アプリケーションやデバイスが応答しなくなる可能性があります。
- **プライバシー侵害**: ユーザーデータやアプリケーションの状態が侵害され、プライバシー侵害や規制違反につながる可能性があります。

## 流入の形態

- **すべてのネットワークインタフェースへのバインド**: アプリケーションを利用可能なすべてのネットワークのインタフェースにバインドするように設定 (ワイルドカードアドレスを使用するなど) し、信頼できないネットワーク経由でもアクセス可能にしています。
- **安全でないループバックアドレスの使用**: 適切なアクセス制限なしでループバックアドレスでリッスンするようにアプリケーションを誤って構成しています。
- **アクセス制御の欠如**: オープンポートを介して公開されるサービスに対して認証および認可のメカニズムを実装していません。
- **デバッグサービスが有効なまま**: 開発またはデバッグ用のネットワークサービスを本番リリースでアクティブなままにしています。
- **ファイアウォール設定の不備**: 適切なファイアウォールルールを設定しておらず、オープンポートへの不正なインバウンド接続を許可しています。

## 緩和策

- **Restrict Network Bindings**: Configure the application to bind only to specific, necessary network interfaces, avoiding the use of wildcard addresses like `INADDR_ANY`.
- **Implement Strong Access Controls**: Enforce authentication and authorization for any services exposed through open ports to ensure only authorized entities can connect.
- **Disable Debugging Services in Production**: Ensure that all development and debugging network services are disabled or removed in production builds.
- **Configure Firewalls Appropriately**: Set up firewall rules to restrict access to open ports, allowing connections only from trusted sources.
