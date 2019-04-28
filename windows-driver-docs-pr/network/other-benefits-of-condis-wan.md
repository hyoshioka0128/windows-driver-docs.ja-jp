---
title: CoNDIS WAN のその他の利点
description: CoNDIS WAN のその他の利点
ms.assetid: 5b937ae4-1486-4563-a863-5c02ba57c7df
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907fb7e326a1349292e9615e6c45a34b44f33c76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378242"
---
# <a name="other-benefits-of-condis-wan"></a>CoNDIS WAN のその他の利点





柔軟性とわかりやすくするため、だけでなくは、WAN いる CoNDIS モデルは、次の利点を提供します。

-   Multipacket をサポートしている CoNDIS WAN ミニポート ドライバー[送信し、受信操作](sending-and-receiving-data.md)します。

-   いる CoNDIS ミニポート ドライバーでは、受信パケットを示します、ときに、バインドされているプロトコルは、パケットの処理を延期できます。 NDIS WAN ミニポート ドライバーでは、受信パケットを示します、ときにバインドされているプロトコルではすぐにデータをコピーする必要があります。

-   いる CoNDIS WAN multipoint 呼び出しをサポートしています。 Multipoint の呼び出しを作成する方法についての詳細については、次を参照してください。[呼び出しを行う](making-a-call.md)します。

-   いる CoNDIS WAN は、サービスの品質 (QoS) をサポートしています。 いる CoNDIS WAN のドライバーを使用して、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 いる CoNDIS QoS の詳細については、次を参照してください。[呼び出しパラメーターの変更を要求する Client-Initiated](client-initiated-request-to-change-call-parameters.md)します。

-   いる CoNDIS WAN のみ、WAN のドライバーに適用される今後の NDIS 拡張機能をサポートします。

 

 





