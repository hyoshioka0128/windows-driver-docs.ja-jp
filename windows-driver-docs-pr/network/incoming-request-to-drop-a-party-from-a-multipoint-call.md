---
title: マルチポイント呼び出しからパーティーを削除するための着信要求
description: マルチポイント呼び出しからパーティーを削除するための着信要求
ms.assetid: 3345f6f6-339f-4349-97fd-9ca9d5b2d241
keywords:
- パーティ WDK
- マルチポイント呼び出し WDK CoNDIS
- multipoint 呼び出しからのパーティの削除
- multipoint 呼び出しからのパーティの削除
- 受信したドロップパーティ要求の WDK CoNDIS 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c31694d0733a230c2ada4a90920a2e318ea4a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843632"
---
# <a name="incoming-request-to-drop-a-party-from-a-multipoint-call"></a>マルチポイント呼び出しからパーティーを削除するための着信要求





通話マネージャーまたは MCM ドライバーは、リモートパーティからの受信要求に対してアラートを受け取り、ネットワークからのメッセージをシグナリングすることで、そのパーティを multipoint 呼び出しから削除します。 また、呼び出しマネージャーまたは MCM ドライバーは、VC でのその他のデータ転送を妨げるネットワークの問題を検出した場合に、パーティを削除するように受信要求を通知することもできます。

呼び出しから削除するパーティが VC の最後のパーティではない場合、呼び出しマネージャーは[**NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingdropparty)を呼び出します。 MCM ドライバーは[**NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingdropparty)を呼び出します。 削除するパーティが VC の最後のパーティである場合、呼び出しマネージャーは[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)を呼び出し、mcm ドライバーは[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall)を呼び出します (呼び出しを閉じるには、「[受信要求」を](incoming-request-to-close-a-call.md)参照してください)。

**Ndis (M) CmDispatchIncomingDropParty**を呼び出すと、ndis によってクライアントの[**ProtocolClIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_drop_party)関数が呼び出されます。

次に示すのは、multipoint 呼び出しを通じてパーティを削除するための呼び出しマネージャーによる受信要求です。

![multipoint 呼び出しを介してパーティを削除するための呼び出しマネージャーによる受信要求を示す図](images/cm-19.png)

次の図は、multipoint 呼び出しを通じてパーティを削除するために、MCM ドライバーを介した受信要求を示しています。

![multipoint 呼び出しを介してパーティを削除するための mcm ドライバーを介した受信要求を示す図](images/fig1-19.png)

*ProtocolClIncomingDropParty*は、クライアントの multipoint VC からパーティを削除するためのプロトコルによって決定された操作を実行する必要があります。 削除するパーティが VC の最後のパーティでない場合、 *ProtocolClIncomingDropParty*は**NdisClDropParty**を呼び出す必要があります (「 [Multipoint 呼び出しからのパーティの削除](dropping-a-party-from-a-multipoint-call.md)」を参照してください)。 削除するパーティが VC の最後のパーティである場合、 *ProtocolClIncomingDropParty*は**NdisClCloseCall**を呼び出す必要があります (「クライアントによって開始された[、呼び出しを閉じる要求」を](client-initiated-request-to-close-a-call.md)参照してください)。

 

 





