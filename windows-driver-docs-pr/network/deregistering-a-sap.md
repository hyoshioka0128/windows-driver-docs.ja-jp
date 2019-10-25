---
title: SAP の登録解除
description: SAP の登録解除
ms.assetid: 2d279348-b58e-4d7e-ac8b-211e9b8a0622
keywords:
- サービスアクセスポイント WDK の接続
- Sap WDK の切断
- Sap の登録解除
- Sap の登録解除
- Sap の削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 051ca43c6e04cce2c1780929482b8980993cace4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834921"
---
# <a name="deregistering-a-sap"></a>SAP の登録解除





[**NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap)を使用する接続指向のクライアント解除。

次の図は、コールマネージャーのクライアントが SAP の登録を解除していることを示しています。

![コールマネージャーのクライアントが sap の登録を解除することを示す図](images/cm-04.png)

次の図は、SAP の登録を解除する MCM ドライバーのクライアントを示しています。

![mcm ドライバーのクライアントが sap の登録を解除したことを示す図](images/fig1-04.png)

**NdisClDeregisterSap**を呼び出すと、NDIS は呼び出しマネージャーまたは mcm ドライバーの[**ProtocolCmDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_deregister_sap)関数を呼び出します。 *ProtocolCmDeregisterSap*では、コールマネージャーまたは mcm ドライバーがネットワーク制御デバイスやその他のメディア固有のエージェントと通信し、ネットワーク上の SAP の登録を解除することがあります。 また、 *ProtocolCmDeregisterSap*は、SAP に対して動的に割り当てられたリソースを解放する必要があります。

*ProtocolCmDeregisterSap*は同期的または非同期的に完了できます。 非同期的に完了するために、呼び出しマネージャーの*ProtocolCmDeregisterSap*関数は[**NdisCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmderegistersapcomplete)を呼び出します。 MCM ドライバーの*ProtocolCmDeregisterSap*関数は、 [**NdisMCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmderegistersapcomplete)を呼び出します。 **Ndis (M) CmdegiProtocolCmDeregisterSap**によって、ndis とクライアントの両方に対して、呼び出しマネージャーが以前に NDIS\_状態を返した SAP 登録解除要求を完了したことが通知され\_行わ.

**Ndis (M) CmDeregisterSapComplete**を呼び出すと、ndis によってクライアントの[**ProtocolClDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_deregister_sap_complete)関数が呼び出されます。 *ProtocolClDeregisterSapComplete*を呼び出すと、クライアントの前の**NdisClDeregisterSap**呼び出しが、呼び出しマネージャーまたは mcm ドライバーによって処理されたことを示します。

クライアントは、その SAP で既に受信されている着信呼び出しに影響を与えずに、その着信呼び出しの VC に影響を与えずに、SAP の登録を解除できます。

 

 





