---
title: CoNDIS WAN のその他の利点
description: CoNDIS WAN のその他の利点
ms.assetid: 5b937ae4-1486-4563-a863-5c02ba57c7df
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01cf14061446710d91a9e80c5360464f2ed378bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366534"
---
# <a name="other-benefits-of-condis-wan"></a>CoNDIS WAN のその他の利点





柔軟性とわかりやすくするため、だけでなくは、WAN いる CoNDIS モデルは、次の利点を提供します。

-   Multipacket をサポートしている CoNDIS WAN ミニポート ドライバー[送信し、受信操作](sending-and-receiving-data.md)します。

-   いる CoNDIS ミニポート ドライバーでは、受信パケットを示します、ときに、バインドされているプロトコルは、パケットの処理を延期できます。 NDIS WAN ミニポート ドライバーでは、受信パケットを示します、ときにバインドされているプロトコルではすぐにデータをコピーする必要があります。

-   いる CoNDIS WAN multipoint 呼び出しをサポートしています。 Multipoint の呼び出しを作成する方法についての詳細については、次を参照してください。[呼び出しを行う](making-a-call.md)します。

-   いる CoNDIS WAN は、サービスの品質 (QoS) をサポートしています。 いる CoNDIS WAN のドライバーを使用して、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 いる CoNDIS QoS の詳細については、次を参照してください。[呼び出しパラメーターの変更を要求する Client-Initiated](client-initiated-request-to-change-call-parameters.md)します。

-   いる CoNDIS WAN のみ、WAN のドライバーに適用される今後の NDIS 拡張機能をサポートします。

 

 





