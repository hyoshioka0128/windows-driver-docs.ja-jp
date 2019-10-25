---
title: 呼び出しパラメーターを変更するためのクライアントが開始した要求
description: 呼び出しパラメーターを変更するためのクライアントが開始した要求
ms.assetid: 1534dbf9-3ee0-490a-9633-55827ffbcb1a
keywords:
- パラメーター変更の呼び出し WDK の変更
- クライアントによって開始された呼び出しパラメーターの変更 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f07ef7fda177a0f97747820dd6e0326bf8e07604
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838201"
---
# <a name="client-initiated-request-to-change-call-parameters"></a>呼び出しパラメーターを変更するためのクライアントが開始した要求





クライアントは、 [**NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos)を使用して、アクティブな仮想接続 (VC) でのサービス品質 (QoS) の変更を要求します。

次の図は、サービス品質の変更を要求している呼び出しマネージャーのクライアントを示しています。

![サービス品質の変更を要求しているコールマネージャーのクライアントを示す図](images/cm-15.png)

次の図は、サービス品質の変更を要求している MCM ドライバーのクライアントを示しています。

![サービス品質の変更を要求している mcm ドライバーのクライアントを示す図](images/fig1-15.png)

**NdisClModifyCallQoS**の呼び出しでは、クライアントは次のものを提供します。

-   VC を識別する*NdisVcHandle*パラメーター。

-   クライアントが要求している呼び出しパラメーターを格納している\_パラメーター構造体への[**CO\_呼び出し**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))を指すポインター。

クライアントが QoS の変化を要求できる状況は、シグナリングプロトコルによって決まります。

**NdisClModifyCallQoS**を呼び出すと、NDIS は call manager または mcm ドライバーの[**Protocolcmmodifycallqos**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_modify_qos_call)関数を呼び出します。この関数は、クライアントが*NDISVCHANDLE*とバッファー内の CO\_呼び出し\_パラメーターの構造を入力します。**NdisClModifyCallQoS**に渡します。 **Protocolcmmodifyqos**は、ネットワーク制御デバイスや、メディアによって使用されるその他のメディア固有のエージェントと通信し、確立された仮想接続のメディア固有の呼び出しパラメーターを変更します。

ネットワークと通信し、変更が成功したことを確認した後、呼び出しマネージャーは[**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc)を呼び出す必要があります (また、mcm ドライバーは[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)を呼び出す必要があります)。これにより、新しい呼び出しパラメーターを使用して、指定された VC をアクティブ化できます。

ネットワークが新しい呼び出しパラメーターを受け入れない場合、または基になるミニポートドライバーがパラメーターを受け入れられない場合、呼び出しマネージャーまたは MCM ドライバーは、変更が試行される前に存在していた状態に VC を復元し、NDIS を返す必要があり\_状態\_エラーです。

クライアントの QoS 変更要求の状態を示すために、呼び出しマネージャーは[**NdisCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmodifycallqoscomplete)を呼び出し、mcm ドライバーは[**NdisMCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmodifycallqoscomplete)を呼び出します。 この呼び出しでは、呼び出しマネージャーまたは MCM ドライバーによって次のように渡されます。

-   要求の状態を示す NDIS\_の状態。

-   VC を識別する*NdisVcHandle* 。

-   VC の呼び出しパラメーターを格納している\_パラメーターの構造体への CO\_呼び出しを指すポインター。

シグナリングプロトコルで許可されている場合、呼び出しマネージャーまたは MCM ドライバーは、変更された呼び出しパラメーターをクライアントに返すことができます。 これらの変更は、ネットワークとのネゴシエーションの製品である場合もあれば、呼び出しマネージャーまたは MCM ドライバー自体によって提供される場合もあります。 呼び出しマネージャーまたは MCM ドライバーは、呼び出しパラメーターが変更されたことを示す必要があります。そのためには、\_パラメーター構造で CO\_呼び出しの\_パラメーター\_CHANGED フラグを設定します。

**Ndis (M) CmModifyCallQoSComplete**の呼び出しが完了すると、ndis はクライアントの[**protocolclmodifycallqoscomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)関数を呼び出します。 NDIS は、次のものを*Protocolclmodifycallqoscomplete*に渡します。

-   QoS を変更するクライアントの要求のステータスを示す NDIS\_の状態。

-   VC を識別する*Protocolvccontext*ハンドル。

-   呼び出しマネージャーまたは MCM ドライバーによって**Ndis (M) CmModifyCallQoSComplete**に渡される呼び出しパラメーターを格納する CO\_呼び出し\_パラメーター構造体へのポインター。

CO\_CALL\_PARAMETERS 構造体で\_PARAMETERS\_CHANGED フラグを呼び出すように設定されている場合、クライアントは返された呼び出しパラメーターを調べて、変更が許容されるかどうかを判断する必要があります。 クライアントの**NdisClModifyCallQoS**への呼び出しが成功した場合、 *Protocolclmodifycallqoscomplete*は制御を返すだけで QoS の変化を受け入れることができます。 そうしないと、 *Protocolclmodifycallqoscomplete*は、シグナル化プロトコルによって許可されている場合、またはクライアントの開発者が可能な renegotiations の数に妥当な制限を設定している限り、呼び出しマネージャーとのさらなる交渉に関与できます。 または、 *Protocolclmodifycallqoscomplete*は、呼び出しマネージャーが QoS を変更する要求を拒否し、以前の状態になったときに、 [**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)で呼び出しを破棄するだけです (「クライアントが開始した[呼び出しを閉じる要求](client-initiated-request-to-close-a-call.md)」を参照してください)。確立された QoS がクライアントに許容できなくなりました。

 

 





