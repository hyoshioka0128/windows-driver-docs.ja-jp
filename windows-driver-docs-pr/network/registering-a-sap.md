---
title: SAP の登録
description: SAP の登録
ms.assetid: 2b318bf0-4f0e-4db7-850b-510a9f2c7cf0
keywords:
- WDK いる CoNDIS のサービス アクセス ポイントします。
- SAPs WDK いる CoNDIS
- SAPs を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff4b626a085a6361a4b26817732fcce738627d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385419"
---
# <a name="registering-a-sap"></a>SAP の登録





クライアントが、受信呼び出しを受け入れる場合、 [ **ProtocolClOpenAfCompleteEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_open_af_complete_ex)関数は、通常 1 つまたは複数の Sap をマネージャーに登録呼び出しを呼び出して[ **NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)します。

次の図は、SAP を登録マネージャーの呼び出しのクライアントを示します。

![sap の登録呼び出し manager のクライアントを示す図](images/cm-02.png)

次の図は、SAP の登録、MCM ドライバーのクライアントを示します。

![mcm ドライバーを使用する sap の登録](images/fig1-02.png)

呼び出しで**NdisClRegisterSap**クライアントが特定の SAP の着信の通知を要求します。 NDIS コール マネージャーのまたは MCM ドライバーのクライアントによって提供される SAP 情報を転送する[ **ProtocolCmRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_reg_sap)関数を検証します。 特定の SAP が既に使用されている場合、または、コール マネージャーまたは MCM ドライバーでクライアントが指定した SAP の仕様が認識されない場合は、コール マネージャーまたは MCM ドライバーには、この要求が失敗します。

*ProtocolCmRegisterSap*、コール マネージャーまたは MCM ドライバーは、ネットワーク デバイスの制御、またはクライアントの接続指向ネットワーク上の SAP を登録するには、他のメディア固有エージェントと通信できます。 *ProtocolCmRegisterSap* NDIS 指定も格納*NdisSapHandle* SAP を表します。

*ProtocolCmRegisterSap*同期または非同期で完了できます。 非同期的に完了する、 *ProtocolCmRegisterSap*コール マネージャーの関数を呼び出す[ **NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregistersapcomplete)します。 *ProtocolCmRegisterSap* MCM ドライバーの関数を呼び出す[ **NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregistersapcomplete)します。 呼び出し**Ndis (M) CmRegisterSapComplete**を呼び出すクライアントの NDIS と[ *ProtocolClRegisterSapComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_register_sap_complete)関数。

場合に、クライアントの呼び出し**NdisClRegisterSap**が成功すると、NDIS クライアントに返されます、SAP を表す、NdisSapHandle します。

そのクライアントを呼び出すことによって、その SAP 宛て受信呼び出しオファーのコール マネージャーには、接続指向のクライアントに代わって SAP がレジスタ後に、通知[ **NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcall)します。 MCM にドライバーを呼び出す[ **NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall)(を参照してください[着信呼び出しを示す](indicating-an-incoming-call.md))。 SAP の登録がまだいる場合でも、クライアントは、SAP の着信を受信できる保留中です。つまり、前にその*ProtocolClRegisterSapComplete*関数が呼び出されます。

 

 





