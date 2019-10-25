---
title: 呼び出しパラメーターを変更するための着信要求
description: 呼び出しパラメーターを変更するための着信要求
ms.assetid: f7b9483c-070e-4a5d-a1b0-fadb65843a1e
keywords:
- パラメーター変更の呼び出し WDK の変更
- 着信呼び出しパラメーターの変更要求の WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff31e45237fc75e2c766410f7fbe5ab3958fe499
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843635"
---
# <a name="incoming-request-to-change-call-parameters"></a>呼び出しパラメーターを変更するための着信要求





呼び出しマネージャーまたは MCM ドライバーは、リモートパーティからの受信要求に対してアラートを受け取り、ネットワークからのメッセージを通知することでアクティブな VC の呼び出しパラメーターを変更します。 呼び出しマネージャーまたは MCM ドライバーがアクティブな呼び出しで動的な QoS 変更をサポートするかどうかは、シグナリングプロトコルによって異なります。

次の図は、呼び出しパラメーターを変更するための呼び出しマネージャーを介した受信要求を示しています。

![呼び出しパラメーターを変更するための呼び出しマネージャーを介した受信要求を示す図](images/cm-16.png)

次の図は、MCM ドライバーを介して呼び出しパラメーターを変更する受信要求を示しています。

![mcm ドライバーを使用して呼び出しパラメーターを変更する着信要求を示す図](images/fig1-16.png)

呼び出しパラメーターを変更するための受信要求を受信すると、コールマネージャーは適切に変更された呼び出しパラメーターを[**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc)に渡して、提案された QoS 変更の基になるミニポートドライバーに通知します。 MCM ドライバーは、変更された呼び出しパラメーターを[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)に渡します (「 [VC のアクティブ化](activating-a-vc.md)」を参照してください)。 基になるミニポートドライバーが変更された呼び出しパラメーターを受け入れる場合、呼び出しマネージャーは[**NdisCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange)を呼び出します (「呼び出しパラメーターを変更するための受信要求」を参照してください)。 MCM ドライバーは[**NdisMCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange)を呼び出します (「呼び出しパラメーターを変更するための受信要求」を参照してください)。 呼び出しマネージャーまたは MCM ドライバーは、 *NdisVcHandle*とバッファーされた[**CO\_呼び出し\_PARAMETERS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体を**Ndis (M) CmDispatchIncomingCallQoSChange**に渡します。

**Ndis (M) CmDispatchIncomingCallQoSChange**を呼び出すと、ndis によってクライアントの[*ProtocolClIncomingCallQoSChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)関数が呼び出されます。 NDIS は、VC および変更された呼び出しパラメーターを識別する*Protocolvccontext*ハンドルを渡します。このハンドルは、バッファーされた CO\_呼び出し\_parameters 構造体を*ProtocolClIncomingCallQoSChange*に呼び出します。

クライアントは、vc の QoS に関して保持する状態を更新し、制御を返す場合を除き、VC の呼び出しパラメーターに対して提案された変更を受け入れます。 提案された変更が受け入れられない場合、クライアントは、シグナリングプロトコルで許可されている場合に、 [**NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos)を使用して呼び出しパラメーターの再ネゴシエーションを試みることができます (「クライアントが開始した[要求を変更する要求](client-initiated-request-to-change-call-parameters.md)」を参照してください)。 それ以外の場合、クライアントは[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を使用して呼び出しを破棄することで、提案された QoS 変更を拒否します (「クライアントが開始した[呼び出しを閉じる要求」を](client-initiated-request-to-close-a-call.md)参照してください)。

**ProtocolClIncomingCallQoS**が返された後、呼び出しマネージャーまたは mcm ドライバーは、クライアントからの提案された変更の受け入れまたは拒否を、要求元のリモートパーティに伝えます。

 

 





