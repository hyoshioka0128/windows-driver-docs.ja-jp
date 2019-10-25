---
title: SAP の登録
description: SAP の登録
ms.assetid: 2b318bf0-4f0e-4db7-850b-510a9f2c7cf0
keywords:
- サービスアクセスポイント WDK の接続
- Sap WDK の切断
- Sap の登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed8fa8f50b6c1dbff3bbbef6fc5adb131d39d591
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842100"
---
# <a name="registering-a-sap"></a>SAP の登録





クライアントが着信呼び出しを受け入れる場合、通常は[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)を呼び出して、呼び出しマネージャーに1つ[**以上の sap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_open_af_complete_ex)を登録します。

次の図は、SAP を登録するコールマネージャーのクライアントを示しています。

![コールマネージャーのクライアントを示す図 (sap の登録)](images/cm-02.png)

次の図は、SAP を登録している MCM ドライバーのクライアントを示しています。

![mcm ドライバーを使用した sap の登録](images/fig1-02.png)

**NdisClRegisterSap**を呼び出すと、クライアントは特定の SAP で着信呼び出しの通知を要求します。 NDIS は、検証のために、クライアントから提供された SAP 情報を呼び出しマネージャーまたは MCM ドライバーの[**Protocolcmregistersap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_reg_sap)関数に転送します。 指定された SAP が既に使用されている場合、または呼び出しマネージャーまたは MCM ドライバーがクライアントによって提供された SAP 仕様を認識しない場合、呼び出しマネージャーまたは MCM ドライバーはこの要求に失敗します。

*Protocolcmregistersap*では、呼び出しマネージャーまたは mcm ドライバーがネットワーク制御デバイスやその他のメディア固有のエージェントと通信し、接続指向クライアントのネットワーク上に SAP を登録する場合があります。 *Protocolcmregistersap*には、sap を表す NDIS によって提供される*NdisSapHandle*も格納されます。

*Protocolcmregistersap*は同期的または非同期的に完了できます。 非同期的に完了するために、呼び出しマネージャーの*Protocolcmregistersap*関数は[**NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregistersapcomplete)を呼び出します。 MCM ドライバーの*Protocolcmregistersap*関数は、 [**NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregistersapcomplete)を呼び出します。 **Ndis (M) Cmregistersap complete**を呼び出すと、ndis によってクライアントの[*protocolclregistersap complete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_register_sap_complete)関数が呼び出されます。

クライアントの**NdisClRegisterSap**への呼び出しが成功した場合、NDIS は SAP を表す NdisSapHandle をクライアントに返します。

呼び出しマネージャーは、接続指向クライアントの代わりに SAP を登録した後、 [**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)を呼び出すことによって、着信呼び出しのクライアントにその sap に転送されることを通知します。 MCM ドライバーは[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)を呼び出します (「[着信呼び出しを示す」を](indicating-an-incoming-call.md)参照してください)。 SAP 登録がまだ保留中であっても、クライアントは SAP で着信呼び出しを受信できます。つまり、 *Protocolclregistersap complete*関数が呼び出される前。

 

 





