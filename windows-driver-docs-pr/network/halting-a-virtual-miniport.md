---
title: 仮想ミニポートの停止
description: 仮想ミニポートの停止
ms.assetid: f53040b1-cbbc-4b13-9bc7-8fae9eb38391
keywords:
- 仮想ミニポートの停止
- 仮想ミニポート WDK ネットワーク
- NDIS 中間ドライバー WDK、仮想ミニポート
- 中間ドライバー WDK ネットワーク、仮想ミニポート
- 仮想ミニポートの停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bb4dcaf9641ba7ad130037e0a489bf54da81f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842119"
---
# <a name="halting-a-virtual-miniport"></a>仮想ミニポートの停止





NDIS 中間ドライバーが[**NdisIMDeinitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance)関数を呼び出すと、ndis は影響を受ける仮想ミニポートに対して[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 通常、中間ドライバーは、 [*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数から**NdisIMDeInitializeDeviceInstance**を呼び出します。

NDIS は、 *HaltAction*パラメーターを**NdisHaltDeviceInstanceDeInitialized**に設定して、ndis が**NdisIMDeInitializeDeviceInstance**関数に対する中間ドライバーの呼び出しに応答してアダプターを停止していることを示します。

中間ドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数は、仮想ミニポートに関連付けられているすべてのドライバー割り当てリソースを解放する必要があります。

 

 





