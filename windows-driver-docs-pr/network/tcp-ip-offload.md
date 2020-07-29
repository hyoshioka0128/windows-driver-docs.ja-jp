---
title: TCP/IP オフロードの概要
description: TCP/IP オフロードの概要
ms.assetid: 1f074ce5-2614-47a5-9ee0-a5e43f05273d
keywords:
- ネットワークドライバー WDK、TCP/IP オフロード
- TCP/IP オフロード WDK ネットワーク
- WDK TCP/IP トランスポートのオフロード
- Tcp/ip オフロード WDK ネットワーク、TCP/IP オフロードについて
- WDK TCP/IP トランスポートのオフロード、TCP/IP オフロードについて
- タスクオフロード WDK TCP/IP トランスポート
- 接続オフロード WDK TCP/IP トランスポート
- パケット WDK ネットワーク、TCP/IP オフロード
ms.date: 06/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 68803e54f329221257f4cb0205918f5e186f718d
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264455"
---
# <a name="tcpip-offload-overview"></a>TCP/IP オフロードの概要

Microsoft TCP/IP トランスポートでは、パフォーマンスを向上させるために、適切な TCP/IP オフロード機能を備えた NIC へのタスクまたは接続をオフロードすることができます。

Windows Vista 以降、Windows オペレーティングシステムでは、次の TCP/IP オフロードサービスがサポートされています。

-   チェックサムタスク

-   アプリケーションのインターネットプロトコルセキュリティ (IPsec) オフロードバージョン1

-   IPsec オフロードバージョン2
    - \[IPsec タスクオフロード機能は非推奨とされており、使用しないでください。\]

-   Large send offload version 1

-   L 送信オフロードバージョン2

-   接続のオフロード

Windows 10 バージョン1912以降では、Windows は UDP セグメント化オフロード (USO) もサポートしています。

Windows Vista 以降で提供される TCP/IP トランスポートでは、IPv4 と IPv6 の両方のパケットに対して TCP/IP オフロードサービスがサポートされています。

NDIS 6.0 以降のミニポートドライバーでは、マルチプロトコルドライバー環境で TCP/IP オフロードサービスがサポートされています。 TCP/IP オフロード対応のミニポートアダプターにバインドされている複数の NDIS 6.0 およびそれ以降のプロトコルドライバーは、TCP/IP オフロードサービスを構成できます。

ここでは、以下の内容について説明します。

-   [TCP/IP オフロードの NET \_ BUFFER \_ LIST 情報へのアクセス](accessing-tcp-ip-offload-net-buffer-list-information.md)
-   [TCP/IP オフロード管理者インターフェイスの使用](using-the-tcp-ip-offload-administrator-interface.md)
-   [オフロード対応ミニポート ドライバーのセキュリティ ガイドライン](security-guidelines-for-offload-capable-miniport-drivers.md)
-   [TCP/IP タスク オフロード](task-offload.md)
-   [接続オフロード](connection-offload.md)

 

 





