---
title: 呼び出しパラメーターを変更するための着信要求
description: 呼び出しパラメーターを変更するための着信要求
ms.assetid: f7b9483c-070e-4a5d-a1b0-fadb65843a1e
keywords:
- WDK いる CoNDIS 呼び出しのパラメーターの変更
- 着信呼び出しのパラメーター変更要求を WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21ba16f8dfea9f351d30e4c4c5383ffb3e9034ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374836"
---
# <a name="incoming-request-to-change-call-parameters"></a>呼び出しパラメーターを変更するための着信要求





コール マネージャーまたは MCM ドライバーに、ネットワークからメッセージを通知することによって、アクティブな VC の呼び出しのパラメーターを変更するリモート パーティから受信要求に警告します。 かどうかをコール マネージャーまたは MCM のドライバーがサポートする QoS の動的な変更アクティブな呼び出しでは、信号のプロトコルに依存します。

次の図は、呼び出しのパラメーターを変更する呼び出しマネージャーにより、受信要求を示します。

![呼び出しのパラメーターを変更する呼び出しマネージャーにより、受信要求を示す図](images/cm-16.png)

次の図は、呼び出しのパラメーターを変更する MCM ドライバーを通じて、受信要求を示します。

![呼び出しのパラメーターを変更する mcm ドライバーを通じて、受信要求を示す図](images/fig1-16.png)

呼び出しのパラメーターを変更する着信要求を受信した後は、コール マネージャーを適切に変更された呼び出しパラメーターを渡します[ **NdisCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmactivatevc)の基になるミニポート ドライバーに通知する、。提案された QoS を変更します。 MCM ドライバーが変更された呼び出しのパラメーターを渡します[ **NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)(を参照してください[VC をアクティブ化する](activating-a-vc.md))。 基になるミニポート ドライバーが変更された呼び出しのパラメーターを受け入れる場合、コール マネージャーは、呼び出し[ **NdisCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange)(呼び出しパラメーターの変更を受信した要求を参照してください)。 MCM にドライバーを呼び出す[ **NdisMCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange)(呼び出しパラメーターの変更を受信した要求を参照してください)。 コール マネージャーまたは MCM ドライバー パスを*NdisVcHandle*をバッファーと[ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体を**Ndis (M) CmDispatchIncomingCallQoSChange**します。

呼び出し**Ndis (M) CmDispatchIncomingCallQoSChange**を呼び出すクライアントの NDIS と[ *ProtocolClIncomingCallQoSChange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)関数。 NDIS 渡します、 *ProtocolVcContext* VC およびバッファー内の CO で変更された呼び出しのパラメーターを識別するハンドル\_呼び出す\_パラメーター構造体を*ProtocolClIncomingCallQoSChange*.

クライアントは、何も可能性があります、VC について、QoS に関する管理状態を更新し、制御を返す以外で、VC の呼び出しのパラメーターに提案された変更を許可します。 クライアントは、呼び出しパラメーターを再ネゴシエートする試行できます提案された変更が許容されない場合[ **NdisClModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos)シグナリング プロトコルによって許可されている場合 (を参照してください[呼び出しのパラメーターを変更する要求を Client-Initiated](client-initiated-request-to-change-call-parameters.md))。 呼び出しの破棄によってそれ以外の場合、クライアントが QoS 変更提案を拒否する[ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)(を参照してください[Client-Initiated の要求の呼び出しを閉じます](client-initiated-request-to-close-a-call.md))。

後**ProtocolClIncomingCallQoS** 、コール マネージャーまたは MCM ドライバーの通信にクライアントの受理または拒否要求を生成したリモート パーティに提案された変更を返します。

 

 





