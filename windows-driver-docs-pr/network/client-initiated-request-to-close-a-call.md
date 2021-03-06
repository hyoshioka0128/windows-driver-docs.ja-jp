---
title: 呼び出しを閉じるためのクライアントが開始した要求
description: 呼び出しを閉じるためのクライアントが開始した要求
ms.assetid: 1eb9c898-086a-463f-a4ae-d5a8727f7d73
keywords:
- close の呼び出しをクライアントが開始した要求の WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2d17fbca159d215a804d055cdec0177f2b135f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385527"
---
# <a name="client-initiated-request-to-close-a-call"></a>呼び出しを閉じるためのクライアントが開始した要求





最初に呼び出す必要がありますが、クライアントには、1 つ以上のパーティがまだ接続されている multipoint 呼び出しが終了している場合、 [ **NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)呼び出し (参照からすべてのドロップが最後のパーティに必要なだけ多くの回数[Multipoint 呼び出しからパーティを削除する](dropping-a-party-from-a-multipoint-call.md))。

クライアントの呼び出しの終了を開始する[ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)します。 次の図は、コール マネージャーを使用して、呼び出しの終了を開始するクライアントを示しています。

![コール マネージャーを使用して、呼び出しの終了を開始するクライアントを示す図](images/cm-20.png)

次の図は、MCM ドライバーを通じて呼び出しの終了を開始するクライアントを示しています。

![mcm ドライバーを通じて呼び出しの終了を開始するクライアントを示す図](images/fig1-20.png)

接続指向のクライアントが呼び出す通常**NdisClCloseCall**次の状況のいずれかで。

-   確立された発信または着信呼び出しを閉じます。

-   [ **ProtocolClIncomingCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_close_call)確立された呼び出しを破棄する関数 (を参照してください[の呼び出しを終了する着信要求](incoming-request-to-close-a-call.md))。

-   [ *ProtocolClIncomingCallQoSChange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)リモート パーティを提案する QoS の変更が許容されない場合は、確立された呼び出しを破棄する関数 (を参照してください[変更を受信した要求パラメーターを呼び出し、](incoming-request-to-change-call-parameters.md))。

-   [ **ProtocolClModifyCallQoSComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)クライアントを提案する QoS の変更を許容できない場合は、リモート パーティに確立された呼び出しを破棄する関数 (を参照してください[呼び出しのパラメーターを変更する要求を Client-Initiated](client-initiated-request-to-change-call-parameters.md))。

クライアントの呼び出し**NdisClCloseCall**と呼び出しを上司に NDIS または MCM ドライバーの[ **ProtocolCmCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_close_call)関数。 *ProtocolCmCloseCall*ローカル ノードとリモート ノード間の接続を終了するネットワーク コントロール デバイスと通信する必要があります。

場合*ProtocolCmCloseCall*を明示的に渡される*CallMgrPartyContext*呼び出しが終了していますが、multipoint 呼び出し。 コール マネージャーまたは MCM ドライバーは、multipoint の呼び出しと呼び出しを終了する、メディアの種類に応じて、ネットワーク ハードウェアと必要なネットワーク通信を実行する必要があります。

NDIS を渡すことができます*ProtocolCmCloseCall*への呼び出しでクライアントによって指定されたデータを格納するバッファーへのポインター **NdisClClose**します。 このデータは、呼び出しが閉じられた理由を示す診断のデータまたはシグナリングのプロトコルに必要なその他のデータを指定できます。 *ProtocolCmCloseCall*呼び出しの終了を完了する前に、ネットワーク経由で、このようなデータを送信する必要があります。 コール マネージャーまたは MCM ドライバーは、NDIS を返す必要がありますの接続を終了すると同時実行データの送信がサポートされていない場合\_状態\_無効な\_データ。

*ProtocolCmCloseCall*で同期的に、多くの場合、非同期的に完了できる[ **NdisCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmclosecallcomplete)(の場合は、コール マネージャー) または[ **NdisMCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmclosecallcomplete)(MCM ドライバーの場合) の場合。 呼び出し**Ndis (M) CmCloseCallComplete**を呼び出すクライアントの NDIS と[ **ProtocolClCloseCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_close_call_complete)関数。

コール マネージャーまたは MCM ドライバーする必要があります VC をそれぞれ呼び出すことによって、呼び出しの使用の非アクティブ化を開始し、 [ **NdisCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc)または[ **NdisMCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc)(を参照してください[VC を非アクティブ化](deactivating-a-vc.md))。 VC (クライアント、コール マネージャー、または MCM ドライバー) の作成者は、開始し、必要に応じて、VC の削除 (を参照してください[VC を削除する](deleting-a-vc.md))。

 

 





