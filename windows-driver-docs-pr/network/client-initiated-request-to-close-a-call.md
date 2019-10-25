---
title: 呼び出しを閉じるためのクライアントが開始した要求
description: 呼び出しを閉じるためのクライアントが開始した要求
ms.assetid: 1eb9c898-086a-463f-a4ae-d5a8727f7d73
keywords:
- クライアントによって開始されたクローズ呼び出し要求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ce9ba9b3240657ef29dd29012e5075e660a734
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835176"
---
# <a name="client-initiated-request-to-close-a-call"></a>呼び出しを閉じるためのクライアントが開始した要求





複数のパーティがまだ接続されているマルチポイント呼び出しをクライアントが終了している場合は、最初に呼び出しから最後のパーティを削除するために必要な回数だけ[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)を呼び出す必要があります (「 [multipoint 呼び出しからのパーティの削除](dropping-a-party-from-a-multipoint-call.md)」を参照してください)。

クライアントは、 [**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を使用して呼び出しの終了を開始します。 次の図は、クライアントが呼び出しマネージャーを使用して呼び出しの終了を開始することを示しています。

![呼び出しマネージャーを使用して呼び出しの終了を開始するクライアントを示す図](images/cm-20.png)

次の図は、MCM ドライバーによる呼び出しの終了をクライアントが開始することを示しています。

![mcm ドライバーを使用して呼び出しの終了を開始するクライアントを示す図](images/fig1-20.png)

通常、接続指向クライアントは、次のいずれかの状況で**NdisClCloseCall**を呼び出します。

-   確立された発信または着信呼び出しを閉じる場合は。

-   [**ProtocolClIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_close_call)関数から、確立された呼び出しを破棄します ([呼び出しを閉じるには、「受信要求」を](incoming-request-to-close-a-call.md)参照してください)。

-   [*ProtocolClIncomingCallQoSChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)関数から、リモートパーティが提案する QoS 変更が許容されない場合に、確立された呼び出しを破棄します (「[呼び出しパラメーターを変更するための受信要求](incoming-request-to-change-call-parameters.md)」を参照してください)。

-   クライアントが提示した QoS の変更がリモートパーティに対して受け入れられない場合に、 [**Protocolclmodifycallqoscomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)関数から、確立された呼び出しを破棄します (「[クライアントが開始した要求の呼び出しパラメーターの変更](client-initiated-request-to-change-call-parameters.md)」を参照してください)。

クライアントから**NdisClCloseCall**への呼び出しによって、NDIS は呼び出しマネージャーまたは mcm ドライバーの[**ProtocolCmCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_call)関数を呼び出します。 *ProtocolCmCloseCall*は、ローカルノードとリモートノード間の接続を終了するために、ネットワークコントロールデバイスと通信する必要があります。

*ProtocolCmCloseCall*に明示的な*CallMgrPartyContext*が渡された場合、終了される呼び出しは multipoint 呼び出しです。 通話マネージャーまたは MCM ドライバーは、メディアの種類に応じて、ネットワークハードウェアとの必要なネットワーク通信を実行して、マルチポイント呼び出しとして呼び出しを終了する必要があります。

NDIS は、 **NdisClClose**への呼び出しでクライアントによって指定されたデータを格納しているバッファーへのポインターを*ProtocolCmCloseCall*に渡すことができます。 このデータは、呼び出しが終了した理由や、シグナリングプロトコルに必要なその他のデータを示す診断データにすることができます。 *ProtocolCmCloseCall*は、呼び出しの終了を完了する前に、このようなデータをネットワーク経由で送信する必要があります。 終了中の接続で同時にデータを送信することがサポートされていない場合、呼び出しマネージャーまたは MCM ドライバーは、無効な\_データ\_NDIS\_の状態を返す必要があります。

*ProtocolCmCloseCall*は、 [**NdisCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete)(呼び出しマネージャーの場合) または[**NdisMCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete)(mcm ドライバーの場合) を使用して同期的または非同期的に完了できます。 **Ndis (M) CmCloseCallComplete**を呼び出すと、ndis によってクライアントの[**ProtocolClCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_close_call_complete)関数が呼び出されます。

呼び出しマネージャーまたは MCM ドライバーは、それぞれ[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)または[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)を呼び出すことによって、呼び出しに使用される vc の非アクティブ化を開始する必要があります (「 [vc の非アクティブ](deactivating-a-vc.md)化」を参照)。 VC (クライアント、コールマネージャー、または MCM ドライバー) の作成者は、必要に応じて VC の削除を開始できます (「 [vc の削除」を](deleting-a-vc.md)参照してください)。

 

 





