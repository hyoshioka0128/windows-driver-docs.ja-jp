---
title: 呼び出しパラメーターを変更するためのクライアントが開始した要求
description: 呼び出しパラメーターを変更するためのクライアントが開始した要求
ms.assetid: 1534dbf9-3ee0-490a-9633-55827ffbcb1a
keywords:
- WDK いる CoNDIS 呼び出しのパラメーターの変更
- クライアントが開始した呼び出しのパラメーターは、WDK いる CoNDIS を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e0bf10fdaba812a0fea23f29b3a2ef40527a372
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374973"
---
# <a name="client-initiated-request-to-change-call-parameters"></a>呼び出しパラメーターを変更するためのクライアントが開始した要求





クライアントで、アクティブな接続 (VC) 上のサービス (QoS) の品質の変更を要求する[ **NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos)します。

次の図は、サービスの品質の変更の要求のコール マネージャーのクライアントを示します。

![サービスの品質の変更の要求のコール マネージャーのクライアントを示す図](images/cm-15.png)

次の図は、サービスの品質の変更の要求、MCM ドライバーのクライアントを示します。

![サービスの品質の変更の要求、mcm ドライバーのクライアントを示す図](images/fig1-15.png)

呼び出しで**NdisClModifyCallQoS**クライアントを提供します。

-   *NdisVcHandle* VC を識別するパラメーター。

-   ポインターを[ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))クライアントが要求呼び出しのパラメーターを含む構造体。

クライアントが QoS の変更を要求する場合は、信号のプロトコルによって決定されます。

呼び出し**NdisClModifyCallQoS**と呼び出しを上司に NDIS または MCM ドライバーの[ **ProtocolCmModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_modify_qos_call)関数は、どの入力、 *NdisVcHandle* 、CO バッファー\_呼び出す\_、クライアントに渡すパラメーターの構造体**NdisClModifyCallQoS**します。 **ProtocolCmModifyQoS**仮想確立された接続のメディア固有の呼び出しのパラメーターを変更する、メディアが行えるように、ネットワーク デバイスの制御、またはその他のメディア固有エージェントと通信します。

ネットワークと通信すると、変更が成功したことを決定する、コール マネージャーを呼び出す必要があります[ **NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmactivatevc)(MCM にドライバーを呼び出す必要がありますと[ **NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)) 新しい呼び出しパラメーターで指定された VC をアクティブ化します。

かどうか、ネットワークが、新しい呼び出しパラメーターを受け入れませんや基になるミニポート ドライバーでは、パラメーターを受け入れることはできません、コール マネージャーまたは MCM ドライバーする必要があります、VC をすべての変更が複数回試行する前に存在していた状態に復元 NDISを返す\_状態\_失敗します。

コール マネージャーは、QoS を変更する、クライアントの要求の状態を示す、 [ **NdisCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmmodifycallqoscomplete)、し、MCM のドライバーを呼び出して[ **NdisMCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmmodifycallqoscomplete)します。 この呼び出しで、コール マネージャーまたは MCM ドライバーに渡します。

-   NDIS\_要求の状態を示す状態。

-   *NdisVcHandle* VC を識別します。

-   CO へのポインター\_呼び出す\_VC の呼び出しのパラメーターを含むパラメーター構造体。

シグナリング プロトコルによって許可されている場合は、クライアントに、コール マネージャーまたは MCM ドライバーが変更された呼び出しパラメーターを渡すことができます。 このような変更は、ネットワークとのネゴシエーションの製品またはコール マネージャーまたは MCM ドライバー自体によってそれらを指定することができます。 コール マネージャーまたは MCM のドライバーの呼び出しを設定して、呼び出しのパラメーターが変更されていることを示す必要があります\_パラメーター\_CO で変更されたフラグ\_呼び出す\_パラメーター構造体。

呼び出し**Ndis (M) CmModifyCallQoSComplete**を呼び出すクライアントの NDIS と[ **ProtocolClModifyCallQoSComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)関数。 NDIS に次のコードに渡します*ProtocolClModifyCallQoSComplete*:

-   NDIS\_QoS を変更する、クライアントの要求の状態を示す状態。

-   A *ProtocolVcContext* VC を識別するハンドル。

-   CO へのポインター\_呼び出す\_コール マネージャーまたは MCM ドライバーによって渡される呼び出しのパラメーターを含むパラメーター構造体**Ndis (M) CmModifyCallQoSComplete**します。

場合、呼び出し\_パラメーター\_CO に変更されたフラグが設定\_呼び出す\_パラメーター構造体、クライアントを確認する必要があります、返されたパラメーターを呼び出すし、変更が許容されるかどうかを判断します。 場合に、クライアントの呼び出し**NdisClModifyCallQoS**成功すると、 *ProtocolClModifyCallQoSComplete* QoS が制御を返すだけで変更を受け入れることができます。 それ以外の場合、 *ProtocolClModifyCallQoSComplete*シグナリング プロトコルによって許可されている場合、クライアントの開発者では、合理的ないくつかの制限を配置可能な限りの数に限り、コール マネージャーでそれ以上のネゴシエーションに関与できますrenegotiations します。 または、 *ProtocolClModifyCallQoSComplete*の呼び出しを破棄できるだけ[ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)(を参照してください[Client-Initiated を要求するには呼び出しを閉じます](client-initiated-request-to-close-a-call.md)) されるたびにコール マネージャーは、QoS を変更する要求を拒否し、以前に確立された QoS は、クライアントに膨大です。

 

 





