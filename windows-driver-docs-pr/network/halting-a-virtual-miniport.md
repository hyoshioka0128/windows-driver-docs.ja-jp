---
title: 仮想ミニポートの停止
description: 仮想ミニポートの停止
ms.assetid: f53040b1-cbbc-4b13-9bc7-8fae9eb38391
keywords:
- 仮想ミニポートを停止します。
- 仮想ミニポート WDK ネットワーク
- NDIS 中間ドライバー WDK、仮想ミニポート
- 中間ドライバー WDK、仮想ネットワークのミニポート
- 仮想ミニポートを停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57852bcba2ea4b12d703303b9ebe6dd3937be2aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379832"
---
# <a name="halting-a-virtual-miniport"></a>仮想ミニポートの停止





場合は、NDIS 中間ドライバの呼び出し、 [ **NdisIMDeinitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)関数では、NDIS 呼び出し、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)影響を受ける仮想ミニポートの関数。 通常、中間ドライバーを呼び出します**NdisIMDeInitializeDeviceInstance**からその[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数。

NDIS セット、 *HaltAction*パラメーターを**NdisHaltDeviceInstanceDeInitialized** NDIS が中間のドライバーの呼び出しに対応のアダプターを停止することを示す、 **NdisIMDeInitializeDeviceInstance**関数。

中間のドライバーの[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数は、仮想ミニポートに関連付けられているすべてのドライバーに割り当てられたリソースを解放する必要があります。

 

 





