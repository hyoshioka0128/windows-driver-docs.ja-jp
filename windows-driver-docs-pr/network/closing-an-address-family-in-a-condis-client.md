---
title: CoNDIS クライアントでアドレス ファミリを閉じる
description: CoNDIS クライアントでアドレス ファミリを閉じる
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- クライアントは、AFs WDK いる CoNDIS を閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86c5e079fd2b4caa1ba4738f045b6ab1e948357e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384209"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>CoNDIS クライアントでアドレス ファミリを閉じる





AFs を閉じるには、いる CoNDIS クライアントが提供する必要があります、 [ **ProtocolClNotifyCloseAf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_notify_close_af)関数。 NDIS 呼び出し*ProtocolClNotifyCloseAf*スタンドアロン コール マネージャーまたは MCM を呼び出すと、 [ **NdisCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)関数または[ **NdisMCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)関数は、それぞれします。

内から*ProtocolClNotifyCloseAf*クライアントでは、指定の AF の終了が完了すると、または、NDIS 返します\_状態\_PENDING と呼び出し、 [ **NdisClNotifyCloseAddressFamilyComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete)操作を完了する関数。 クライアントの呼び出し後**NdisClNotifyCloseAddressFamilyComplete**、NDIS 呼び出し、 [ **ProtocolCmNotifyCloseAfComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_notify_close_af_complete)コール マネージャーに通知する関数をクライアントでは、AF が閉じられます。

AF を閉じるには、クライアントが必要です。

1.  クライアントに multipoint のアクティブな接続がある場合は、呼び出し、 [ **NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)単一のパーティのみが各 multipoint 接続 (VC) でアクティブなままになるまでに必要な回数として機能します。

2.  呼び出す、 [ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)閉じますすべての呼び出しに必要な回数がまだ開いているとおりに機能し、は、アドレス ファミリに関連付けられます。

3.  呼び出す、 [ **NdisClDeregisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)すべてのサービスへのアクセス ポイント (Sap)、クライアントが、コール マネージャーに登録されている登録の解除に必要な回数として機能します。

4.  呼び出す、 [ **NdisClCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily) AF を閉じます。

 

 





