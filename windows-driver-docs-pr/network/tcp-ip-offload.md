---
title: TCP/IP オフロード
description: TCP/IP オフロード
ms.assetid: 1f074ce5-2614-47a5-9ee0-a5e43f05273d
keywords:
- ネットワーク ドライバー WDK では、TCP/IP の負荷を軽減します。
- TCP/IP オフロード WDK ネットワーク
- WDK TCP/IP トランスポートの負荷を軽減します。
- TCP/IP のオフロードの詳細について、オフロード WDK の TCP/IP のネットワーク、
- TCP/IP のオフロードは、WDK TCP/IP トランスポートの負荷を軽減します。
- タスクのオフロード WDK TCP/IP トランスポート
- WDK TCP/IP トランスポート接続の負荷を軽減します。
- パケット WDK ネットワー キング、TCP/IP のオフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5924e6c230c51f5a84a4028b3eb610748941266f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350831"
---
# <a name="tcpip-offload"></a>TCP/IP オフロード





そのパフォーマンスを向上させるのには、Microsoft TCP/IP トランスポートはタスクまたは適切な TCP/IP オフロード機能を備えている NIC への接続をオフロードできます。

Windows Vista 以降、Windows オペレーティング システムのサポートしている次の TCP/IP のオフロード サービス。

-   チェックサム タスク

-   アプリケーションのインターネット プロトコル セキュリティ (IPsec) は、バージョン 1 をオフロードします。

-   IPsec オフロード バージョン 2
    - \[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

-   大量送信オフロード バージョン 1

-   大量送信オフロード バージョン 2

-   接続のオフロード

Windows Vista 以降を装備されている TCP/IP トランスポートは、IPv4 と IPv6 の両方のパケットの TCP/IP のオフロード サービスをサポートします。

NDIS 6.0 とそれ以降のミニポート ドライバーは、複数のプロトコル ドライバー環境で TCP/IP オフロード サービスをサポートします。 複数の NDIS 6.0 と TCP/IP のオフロード対応ミニポート アダプターにバインドされている以降のプロトコル ドライバーには、TCP/IP オフロード サービスを構成できます。

このセクションの内容:

-   [NET TCP/IP にアクセスする負荷を軽減\_バッファー\_情報を一覧表示](accessing-tcp-ip-offload-net-buffer-list-information.md)
-   [TCP/IP のオフロード管理者インターフェイスを使用します。](using-the-tcp-ip-offload-administrator-interface.md)
-   [オフロード対応ミニポート ドライバーのセキュリティ ガイドライン](security-guidelines-for-offload-capable-miniport-drivers.md)
-   [TCP/IP タスク オフロード](task-offload.md)
-   [接続のオフロード](connection-offload.md)

 

 





