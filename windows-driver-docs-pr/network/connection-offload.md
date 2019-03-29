---
title: 接続オフロード
description: 接続オフロード
ms.assetid: 4c1b1a98-6ad3-4817-9e3d-d6112c887352
keywords:
- WDK TCP/IP トランスポート接続の負荷を軽減します。
- TCP/IP のオフロード WDK のネットワー キング、接続のオフロード
- WDK TCP/IP トランスポート、接続のオフロードをオフロードします。
- 接続のオフロード WDK TCP/IP トランスポートは、接続のオフロードの詳細について
- 機能 WDK TCP/IP の負荷を軽減します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf445931229909edb60544d2ac2a785a5e3ce914
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570725"
---
# <a name="connection-offload"></a>接続オフロード





パフォーマンスを向上させるには、Microsoft TCP/IP トランスポートは接続されている、適切な TCP/IP - オフロード機能 NIC への接続をオフロードできます。

NDIS 接続のオフロード インターフェイスは、接続の構成を有効にするフック オフロード TCP chimney オフロードなどのサービスを提供します。 NDIS でオフロード サービスの接続の詳細については、次を参照してください。 [TCP/IP 接続のオフロード](offloading-tcp-ip-connections.md)します。

TCP chimney オフロード サービスは、NDIS 6.0 以降でサポートされています。

このセクションの内容:

-   [接続のオフロード機能を判断します。](determining-connection-offload-capabilities.md)
-   [NIC の接続のオフロード機能の報告](reporting-a-nic-s-connection-offload-capabilities.md)
-   [オフロード サービスを有効にして、接続を無効化](enabling-and-disabling-connection-offload-services.md)
-   [現在の接続のオフロード設定を決定します。](determining-the-current-connection-offload-settings.md)
-   [レジストリ値を使用して、接続のオフロードを無効にするには](using-registry-values-to-enable-and-disable-connection-offloading.md)
-   [TCP/IP 接続のオフロード](offloading-tcp-ip-connections.md)

 

 





