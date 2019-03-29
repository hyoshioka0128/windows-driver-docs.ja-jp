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
ms.openlocfilehash: 6e808d8171210c2b1fc70a4f7cd27f308a169a7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579405"
---
# <a name="halting-a-virtual-miniport"></a>仮想ミニポートの停止





場合は、NDIS 中間ドライバの呼び出し、 [ **NdisIMDeinitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562721)関数では、NDIS 呼び出し、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)影響を受ける仮想ミニポートの関数。 通常、中間ドライバーを呼び出します**NdisIMDeInitializeDeviceInstance**からその[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。

NDIS セット、 *HaltAction*パラメーターを**NdisHaltDeviceInstanceDeInitialized** NDIS が中間のドライバーの呼び出しに対応のアダプターを停止することを示す、 **NdisIMDeInitializeDeviceInstance**関数。

中間のドライバーの[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数は、仮想ミニポートに関連付けられているすべてのドライバーに割り当てられたリソースを解放する必要があります。

 

 





