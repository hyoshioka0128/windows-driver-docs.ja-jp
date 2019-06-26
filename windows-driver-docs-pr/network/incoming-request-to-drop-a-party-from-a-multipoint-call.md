---
title: マルチポイント呼び出しからパーティーを削除するための着信要求
description: マルチポイント呼び出しからパーティーを削除するための着信要求
ms.assetid: 3345f6f6-339f-4349-97fd-9ca9d5b2d241
keywords:
- パーティ WDK いる CoNDIS
- multipoint 呼び出し WDK いる CoNDIS
- multipoint 呼び出しからパーティを削除しています
- multipoint 呼び出しからパーティを削除します。
- ドロップ パーティが受信要求の WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bd3c784ded5fd6059bb590acfeb252d6476d0cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374853"
---
# <a name="incoming-request-to-drop-a-party-from-a-multipoint-call"></a>マルチポイント呼び出しからパーティーを削除するための着信要求





コール マネージャーまたは MCM ドライバーで multipoint 呼び出しから、ネットワークからメッセージを通知することによって、パーティを削除するリモート パーティから受信要求に発生します。 コール マネージャーまたは MCM ドライバーでは、受信要求をさらに、VC 上のデータ転送を妨げるネットワーク問題を検出した場合は、パーティを削除することも通知できます。

呼び出しから削除されるパーティがない場合、VC の最後のパーティ、コール マネージャー呼び出します[ **NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingdropparty)します。 MCM にドライバーを呼び出す[ **NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingdropparty)します。 コール マネージャーは、パーティを削除中ですが、VC の最後のパーティである場合は、 [ **NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingclosecall)、し、MCM のドライバーを呼び出して[ **NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingclosecall)(を参照してください[の呼び出しを終了する着信要求](incoming-request-to-close-a-call.md))。

呼び出し**Ndis (M) CmDispatchIncomingDropParty**を呼び出すクライアントの NDIS と[ **ProtocolClIncomingDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_drop_party)関数。

次に示しますを呼び出すことによって、受信要求 multipoint 呼び出しを通じて、パーティを削除するマネージャー。

![multipoint の呼び出しでパーティを削除するコール マネージャーにより、受信要求を示す図](images/cm-19.png)

次の図は、multipoint の呼び出しでパーティを削除する MCM ドライバーを通じて、受信要求を示します。

![multipoint の呼び出しでパーティを削除する mcm ドライバーを通じて、受信要求を示す図](images/fig1-19.png)

*ProtocolClIncomingDropParty*プロトコルにより決定されたクライアントの multipoint VC からパーティを削除する操作を実行する必要があります。 パーティを削除中ですが、VC の最後のパーティではない場合*ProtocolClIncomingDropParty*呼び出す必要があります**NdisClDropParty**(を参照してください[Multipoint 呼び出しからパーティを削除する](dropping-a-party-from-a-multipoint-call.md)). パーティを削除する場合、VC の最後のパーティ*ProtocolClIncomingDropParty*呼び出す必要があります**NdisClCloseCall**(を参照してください[Client-Initiated の要求の呼び出しを閉じます](client-initiated-request-to-close-a-call.md))。

 

 





