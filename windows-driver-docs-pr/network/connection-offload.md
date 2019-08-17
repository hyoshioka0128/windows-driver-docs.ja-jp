---
title: 接続のオフロードの概要
description: 接続のオフロードの概要
ms.assetid: 4c1b1a98-6ad3-4817-9e3d-d6112c887352
keywords:
- 接続オフロード WDK TCP/IP トランスポート
- TCP/IP オフロード WDK ネットワーク、接続オフロード
- WDK TCP/IP トランスポートのオフロード、接続のオフロード
- 接続オフロード WDK TCP/IP トランスポート、接続オフロードについて
- 機能 WDK TCP/IP オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5f850b8785ec0ccc4537026bd58c95d4c269c96
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565762"
---
# <a name="connection-offload-overview"></a>接続のオフロードの概要





パフォーマンスを向上させるために、Microsoft TCP/IP トランスポートは、適切な TCP/IP 接続オフロード機能を備えた NIC への接続をオフロードすることができます。

NDIS 接続オフロードインターフェイスには、TCP chimney オフロードなどの接続オフロードサービスの構成を有効にするフックが用意されています。 NDIS の接続オフロードサービスの詳細については、「 [Tcp/ip 接続のオフロード](offloading-tcp-ip-connections.md)」を参照してください。

TCP chimney オフロードサービスは、NDIS 6.0 以降でサポートされています。

このセクションの内容:

-   [接続のオフロード機能の決定](determining-connection-offload-capabilities.md)
-   [NIC の接続オフロード機能の報告](reporting-a-nic-s-connection-offload-capabilities.md)
-   [接続オフロードサービスの有効化と無効化](enabling-and-disabling-connection-offload-services.md)
-   [現在の接続のオフロード設定を確認しています](determining-the-current-connection-offload-settings.md)
-   [レジストリ値を使用した接続オフロードの有効化と無効化](using-registry-values-to-enable-and-disable-connection-offloading.md)
-   [TCP/IP 接続のオフロード](offloading-tcp-ip-connections.md)

 

 





