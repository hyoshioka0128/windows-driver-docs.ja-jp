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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c55134ba2d320e4791dbb412a6450ca45bfd1f6
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565634"
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

Windows Vista 以降で提供される TCP/IP トランスポートでは、IPv4 と IPv6 の両方のパケットに対して TCP/IP オフロードサービスがサポートされています。

NDIS 6.0 以降のミニポートドライバーでは、マルチプロトコルドライバー環境で TCP/IP オフロードサービスがサポートされています。 TCP/IP オフロード対応のミニポートアダプターにバインドされている複数の NDIS 6.0 およびそれ以降のプロトコルドライバーは、TCP/IP オフロードサービスを構成できます。

このセクションの内容:

-   [Tcp/ip オフロードの NET\_BUFFER\_LIST 情報へのアクセス](accessing-tcp-ip-offload-net-buffer-list-information.md)
-   [TCP/IP オフロード管理者インターフェイスの使用](using-the-tcp-ip-offload-administrator-interface.md)
-   [オフロード対応ミニポートドライバーのセキュリティガイドライン](security-guidelines-for-offload-capable-miniport-drivers.md)
-   [TCP/IP タスクオフロード](task-offload.md)
-   [接続のオフロード](connection-offload.md)

 

 





