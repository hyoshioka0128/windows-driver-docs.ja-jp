---
title: SAP の登録解除
description: SAP の登録解除
ms.assetid: 2d279348-b58e-4d7e-ac8b-211e9b8a0622
keywords:
- WDK いる CoNDIS のサービス アクセス ポイントします。
- SAPs WDK いる CoNDIS
- SAPs の登録を解除
- SAPs の登録を解除
- SAPs を削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13cab6798f8c26fb5921f49dac0e737ae43eb8f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384573"
---
# <a name="deregistering-a-sap"></a>SAP の登録解除





接続指向のクライアントでの SAP の登録を解除[ **NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)します。

次の図は、マネージャーは、SAP の登録解除の呼び出しのクライアントを示します。

![sap の登録を解除コール マネージャーのクライアントを示す図](images/cm-04.png)

次の図は、SAP の登録を解除、MCM ドライバーのクライアントを示します。

![sap の登録を解除、mcm ドライバーのクライアントを示す図](images/fig1-04.png)

呼び出し**NdisClDeregisterSap**と呼び出しを上司に NDIS または MCM ドライバーの[ **ProtocolCmDeregisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_deregister_sap)関数。 *ProtocolCmDeregisterSap*、コール マネージャーまたは MCM ドライバーは、ネットワーク デバイスの制御や、ネットワーク上の SAP の登録を解除するには、他のメディア固有エージェントと通信できます。 さらに、 *ProtocolCmDeregisterSap* sap 動的に割り当てられているリソースを解放する必要があります。

*ProtocolCmDeregisterSap*同期または非同期で完了できます。 非同期的に完了する、 *ProtocolCmDeregisterSap*コール マネージャーの関数を呼び出す[ **NdisCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmderegistersapcomplete)します。 *ProtocolCmDeregisterSap* MCM ドライバーの関数を呼び出す[ **NdisMCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmderegistersapcomplete)します。 **Ndis (M) CmDegisterSapComplete** NDIS とクライアントの両方の通知、コール マネージャーでの SAP 登録解除要求が完了したこと、 *ProtocolCmDeregisterSap* NDIS以前に返した関数\_ステータス\_保留します。

呼び出し**Ndis (M) CmDeregisterSapComplete**を呼び出すクライアントの NDIS と[ **ProtocolClDeregisterSapComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_deregister_sap_complete)関数。 呼び出し*ProtocolClDeregisterSapComplete*クライアントへの呼び出しの前のことを示します**NdisClDeregisterSap**コール マネージャーまたは MCM ドライバーによって処理されました。

その SAP で受信されている着信呼び出しの影響を与えずに、その着信呼び出しの VC の影響を与えずに、クライアントに SAP を解除できますに注意してください。

 

 





