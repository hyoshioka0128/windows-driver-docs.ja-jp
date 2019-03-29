---
title: ミニポート ドライバーについて
description: ミニポート ドライバーについて
ms.assetid: faaeee13-7d21-4e06-a33c-da249716d925
keywords:
- コネクションレス ドライバー WDK ネットワーク
- 接続指向のドライバー WDK ネットワーク
- WAN ミニポート ドライバー WDK ネットワーク
- ミニポート ドライバー WDK ネットワーク、WAN ミニポート ドライバー
- NDIS ミニポート ドライバー WDK、WAN ミニポート ドライバー
- ミニポート ドライバー WDK ネットワー キング、ミニポート ドライバー WDM 下端が
- NDIS ミニポート ドライバー WDK、ミニポート ドライバー WDM が削減エッジ
- WDM 低い edge WDK ネットワーク
- ミニポート ドライバー WDK ネットワー キング、IrDA ミニポート ドライバー
- NDIS ミニポート ドライバー WDK、IrDA ミニポート ドライバー
- IrDA ドライバー WDK ネットワーク
- ミニポート ドライバー WDK ネットワークでスケーラブルなネットワー キングのサポート
- NDIS ミニポート ドライバー WDK、スケーラブルなネットワー キングのサポート
- ネットワーク ドライバー WDK、種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1384d03543b91995b46f11e04e7dac9032366573
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580330"
---
# <a name="learning-about-miniport-drivers"></a>ミニポート ドライバーについて





いくつかの種類のミニポート ドライバーがあります。 次の一覧では、WDK ドキュメントのセクションをお読みください、書き込みを行っているミニポート ドライバーの種類に応じてについて説明します。

<a href="" id="connectionless-miniport-drivers"></a>**コネクションレスのミニポート ドライバー**  
コネクションレス型ネットワークのメディア (イーサネット) などのネットワーク インターフェイス カード (NIC) を制御するミニポート ドライバーを作成する場合は、次の読み取り。

-   [NDIS ミニポート ドライバーの概要](introduction-to-ndis-miniport-drivers.md)

-   [NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)

<a href="" id="connection-oriented-miniport-drivers"></a>**接続指向のミニポート ドライバー**  
接続指向ネットワークのメディア (ISDN) などのミニポート ドライバーを作成する場合は、次の読み取り。

-   すべての「コネクションレス ミニポート ドライバー」 の下には、このトピックに記載されているセクション

-   [接続指向の NDIS](connection-oriented-ndis.md)

<a href="" id="wan-miniport-drivers"></a>**WAN ミニポート ドライバー**  
ワイド エリア ネットワーク (WAN) の NIC を制御するミニポート ドライバーを作成する場合は、次の読み取り。

-   すべての「コネクションレス ミニポート ドライバー」 の下には、このトピックに記載されているセクション

-   [WAN ミニポート ドライバー](wan-miniport-drivers.md)

<a href="" id="miniports-with-a-wdm-lower-interface"></a>**WDM 低いインターフェイスを備えたミニポート**  
他のカーネル ドライバー インターフェイスで Microsoft Windows Driver Model (WDM) の下のインターフェイスを備えたミニポート ドライバーを作成する場合は、次の読み取り。

-   すべての「コネクションレス ミニポート ドライバー」 の下には、このトピックに記載されているセクション

-   [ミニポート ドライバー WDM がインターフェイスを削減します。](miniport-drivers-with-a-wdm-lower-interface.md)

<a href="" id="irda-miniport-drivers"></a>**IrDA ミニポート ドライバー**  
IrDA アダプターを制御するミニポート ドライバーを作成する場合は、次の読み取り。

-   すべての「コネクションレス ミニポート ドライバー」 の下には、このトピックに記載されているセクション

<a href="" id="miniport-drivers-that-support-scalable-networking"></a>**スケーラブルなネットワークをサポートするミニポート ドライバー**  
スケーラブルなネットワークをサポートするミニポート ドライバーの詳細については、次のようになります。

-   [スケーラブル ネットワーク](https://msdn.microsoft.com/library/windows/hardware/ff570735)

<a href="" id="miniport-drivers-that-support-offloading-tcp-ip--------to-hardware-------"></a>**TCP/IP をハードウェアにオフロードをサポートするミニポート ドライバー**   
TCP/IP をハードウェアにオフロード ミニポート ドライバーの詳細については、次のようになります。

-   [TCP/IP のオフロード](tcp-ip-offload.md)

 

 





