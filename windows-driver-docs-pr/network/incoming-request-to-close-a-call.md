---
title: 呼び出しを閉じるための着信要求
description: 呼び出しを閉じるための着信要求
ms.assetid: ecdcb74d-6151-4e2b-8fe7-95f455f4deb4
keywords:
- 受信したクローズ呼び出し要求の WDK の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6891838bcbe172aa51ca7b0296b7f4ce4fed35b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843634"
---
# <a name="incoming-request-to-close-a-call"></a>呼び出しを閉じるための着信要求





リモートクライアントが呼び出しを終了する場合、ローカル呼び出しマネージャーまたは MCM ドライバーは、この受信要求をローカルクライアントに示す必要があります。 このような要求を示すために、呼び出しマネージャーは*Closestatus*が NDIS\_STATUS\_SUCCESS に設定された[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)を呼び出します (次の図を参照)。

![呼び出しを閉じるための呼び出しマネージャーを介した受信要求を示す図 ](images/cm-22.png)

MCM ドライバーは、呼び出しを閉じるための受信要求を示すために[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall)を呼び出します (次の図を参照してください)。

![呼び出しを閉じるために mcm ドライバーを介した受信要求を示す図 ](images/fig1-22.png)

また、呼び出しマネージャーまたは MCM ドライバーは、 **Ndis (M) CmDispatchIncomingCloseCall**を呼び出すこともできます。

-   呼び出しマネージャーまたは MCM によって示されている着信呼び出しに応答して、接続指向クライアントが呼び出しパラメーターで許容できない変更を要求している場合、その[**Protocolcmincomingcallcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_incoming_call_complete)関数から。ドライバー (「[呼び出しパラメーターを変更するための受信要求」を](incoming-request-to-change-call-parameters.md)参照してください)。

-   ネットワークの状態が異常な場合は、呼び出しマネージャーがアクティブな呼び出しを破棄するように強制します。

**Ndis (M) CmDispatchIncomingCloseCall**を呼び出すと、ndis はその接続で接続指向クライアントの[**ProtocolClIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_close_call)関数を呼び出します。 *ProtocolClIncomingCloseCall*は、接続が切断されていることを自身のクライアントまたはクライアントに通知するなど、プロトコルによって決定された操作を実行する必要があります。 Closed の呼び出しがクライアントによって作成された multipoint VC である場合、 *ProtocolClIncomingCloseCall*は、1つのパーティのみが VC にとどまるまで[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)を1回以上呼び出す必要があります (「 [multipoint 呼び出しからのパーティの削除](dropping-a-party-from-a-multipoint-call.md)」を参照してください)。

次に、 *ProtocolClIncomingCloseCall*は、クライアントが送信または受信しようとしていないことを確認するために、 [**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)(vc がクライアントによって作成された multipoint vc の場合は、vc の最後のパーティへのハンドルを持つ) を呼び出す必要があります。この特定の VC。 呼び出しマネージャーまたは MCM ドライバーがこの VC を作成した場合、 *ProtocolClIncomingCloseCall*は**NdisClCloseCall**を呼び出した後に制御を返す必要があります。 また、呼び出しマネージャーまたは MCM ドライバーも VC を非アクティブ化する必要があります (「 [vc の非アクティブ](deactivating-a-vc.md)化」を参照してください)。

クライアントが最初にこの VC を送信呼び出し用に作成し、 *closestatus*が NDIS\_STATUS\_SUCCESS の場合、 *ProtocolClIncomingCloseCall*は必要に応じて、 [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)で vc を破棄できます (「 [vc の削除](deleting-a-vc.md)」を参照してください)。) を使用するか、別の呼び出しに対して VC を再利用します。 *Closestatus*が NDIS\_STATUS\_SUCCESS でない場合、 *ProtocolClIncomingCloseCall*は**NdisCoDeleteVc**を呼び出す必要があります。

呼び出しマネージャーまたは MCM ドライバーが着信呼び出し用にこの VC を最初に作成した場合、呼び出しマネージャーまたは MCM ドライバーは、必要に応じて、 **NdisCoDeleteVc**または[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)を呼び出すことで[vc を削除](deleting-a-vc.md)できます。

 

 





