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

- **Unauthorized Access**: Attackers can connect to open ports and gain access to application functionalities or sensitive data.
- **Data Leakage**: Sensitive information may be exposed through unprotected ports if proper authentication and encryption are not enforced.
- **Remote Code Execution**: Exploitation of open ports can lead to the execution of arbitrary code on the device.
- **Denial of Service**: Attackers may overload the open port, causing the application or device to become unresponsive.
- **Privacy Breach**: User data and application state can be compromised, leading to privacy violations and non-compliance with regulations.

## 流入の形態

- **Binding to All Network Interfaces**: Configuring the application to bind to all available network interfaces (e.g., using wildcard addresses), making it accessible over untrusted networks.
- **Insecure Loopback Address Usage**: Misconfiguring the application to listen on loopback addresses without proper access restrictions.
- **Lack of Access Controls**: Failing to implement authentication and authorization mechanisms for services exposed via open ports.
- **Debug Services Left Enabled**: Leaving development or debugging network services active in production releases.
- **Misconfigured Firewall Settings**: Not setting up proper firewall rules, allowing unauthorized inbound connections to open ports.

## 緩和策

- **Restrict Network Bindings**: Configure the application to bind only to specific, necessary network interfaces, avoiding the use of wildcard addresses like `INADDR_ANY`.
- **Implement Strong Access Controls**: Enforce authentication and authorization for any services exposed through open ports to ensure only authorized entities can connect.
- **Disable Debugging Services in Production**: Ensure that all development and debugging network services are disabled or removed in production builds.
- **Configure Firewalls Appropriately**: Set up firewall rules to restrict access to open ports, allowing connections only from trusted sources.
