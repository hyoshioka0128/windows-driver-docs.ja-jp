---
title: ミニポート ドライバーについて
description: ミニポート ドライバーについて
ms.assetid: faaeee13-7d21-4e06-a33c-da249716d925
keywords:
- コネクションレスドライバー WDK ネットワーク
- 接続指向ドライバー WDK ネットワーク
- WAN ミニポートドライバーの WDK ネットワーク
- ミニポートドライバー WDK ネットワーク、WAN ミニポートドライバー
- NDIS ミニポートドライバー WDK、WAN ミニポートドライバー
- ミニポートドライバー WDK ネットワーク, ミニポートドライバー (WDM)
- NDIS ミニポートドライバー、WDM を使用したミニポートドライバー
- WDM 低エッジの WDK ネットワーク
- ミニポートドライバー WDK ネットワーク、IrDA ミニポートドライバー
- NDIS ミニポートドライバー WDK、IrDA ミニポートドライバー
- IrDA ドライバー WDK ネットワーク
- ミニポートドライバー WDK ネットワーク、スケーラブルなネットワークサポート
- NDIS ミニポートドライバー WDK、スケーラブルなネットワークサポート
- ネットワークドライバー WDK、種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33bcfc001801a71d86873737595281f33c37059c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844147"
---
# <a name="learning-about-miniport-drivers"></a>ミニポート ドライバーについて





ミニポートドライバーにはいくつかの種類があります。 次の一覧は、作成するミニポートドライバーの種類に応じて、読み取る必要がある WDK ドキュメントのセクションを示しています。

<a href="" id="connectionless-miniport-drivers"></a>**コネクションレスミニポートドライバー**  
コネクションレスネットワークメディア (イーサネットなど) 用のネットワークインターフェイスカード (NIC) を制御するミニポートドライバーを作成する場合は、次のドキュメントを参照してください。

-   [NDIS ミニポートドライバーの概要](introduction-to-ndis-miniport-drivers.md)

-   [NDIS ミニポートドライバー](writing-ndis-miniport-drivers.md)

<a href="" id="connection-oriented-miniport-drivers"></a>**接続指向ミニポートドライバー**  
接続指向のネットワークメディア (ISDN など) 用のミニポートドライバーを作成する場合は、次のドキュメントを参照してください。

-   このトピックの「コネクションレスミニポートドライバー」に記載されているすべてのセクション

-   [接続指向の NDIS](connection-oriented-ndis.md)

<a href="" id="wan-miniport-drivers"></a>**WAN ミニポートドライバー**  
ワイドエリアネットワーク (WAN) NIC を制御するミニポートドライバーを作成する場合は、次のドキュメントを参照してください。

-   このトピックの「コネクションレスミニポートドライバー」に記載されているすべてのセクション

-   [WAN ミニポートドライバー](wan-miniport-drivers.md)

<a href="" id="miniports-with-a-wdm-lower-interface"></a>**WDM インターフェイスがあるミニポート**  
他のカーネルドライバーにインターフェイスするミニポートドライバーを作成しており、Microsoft Windows Driver Model (WDM) 下位インターフェイスを備えている場合は、次のようにします。

-   このトピックの「コネクションレスミニポートドライバー」に記載されているすべてのセクション

-   [WDM インターフェイスがあるミニポートドライバー](miniport-drivers-with-a-wdm-lower-interface.md)

<a href="" id="irda-miniport-drivers"></a>**IrDA ミニポートドライバー**  
IrDA アダプターを制御するミニポートドライバーを作成する場合は、次のドキュメントを参照してください。

-   このトピックの「コネクションレスミニポートドライバー」に記載されているすべてのセクション

<a href="" id="miniport-drivers-that-support-scalable-networking"></a>**スケーラブルなネットワークをサポートするミニポートドライバー**  
スケーラブルなネットワークをサポートするミニポートドライバーの詳細については、以下を参照してください。

-   [スケーラブル ネットワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

<a href="" id="miniport-drivers-that-support-offloading-tcp-ip--------to-hardware-------"></a>**ハードウェアへの tcp/ip のオフロードをサポートするミニポートドライバー**   
TCP/IP をハードウェアにオフロードするミニポートドライバーの詳細については、次を参照してください。

-   [TCP/IP オフロード](tcp-ip-offload.md)

 

 





