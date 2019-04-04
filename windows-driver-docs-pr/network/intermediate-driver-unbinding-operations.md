---
title: 中間のドライバーが操作をバインド解除
description: 中間のドライバーが操作をバインド解除
ms.assetid: d316385a-9481-4708-9e09-06d0424acd8f
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK, バインド
- バインド解除の WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3a34b76497ea9480976ab3a1937b98d6aabec9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548880"
---
# <a name="intermediate-driver-unbinding-operations"></a>中間のドライバーが操作をバインド解除





中間のドライバーを呼び出すことによって、基になるミニポート ドライバーからバインド解除[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)からその[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。 NDIS 呼び出し*ProtocolUnbindAdapterEx*場合は、基になるミニポート アダプターが使用できなくします。

中間のドライバーの*ProtocolUnbindAdapterEx*関数は、ドライバーに未処理の呼び出し時に呼び出される可能性があります[ **NdisIMInitializeDeviceInstanceEx**](https://msdn.microsoft.com/library/windows/hardware/ff562727)します。 このような状況は、NDIS がまだ呼び出されていないときに発生します。 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)を対応する仮想 miniports を初期化します。 この場合、中間のドライバーを呼び出す必要があります[ **NdisIMCancelInitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562719)しようとすると、これらの仮想ミニポートの初期化をキャンセルします。

終了バインドは、中間のドライバーによってエクスポートされたデバイスにマップされている場合、そのデバイスは、呼び出すことによって初期化された場合[ **NdisIMInitializeDeviceInstanceEx**](https://msdn.microsoft.com/library/windows/hardware/ff562727)、中間ドライバーを呼び出すことができます[ **NdisIMDeInitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562721)デバイスを閉じます。 仮想ミニポートのドライバーの中間になりますまたはより高度なドライバーによって行われた要求の送信に使用できる不要になったことになります。

場合は、NDIS 中間ドライバの呼び出し、 **NdisIMDeInitializeDeviceInstance**関数では、NDIS 呼び出し、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)の影響を受ける仮想ミニポート関数. 仮想ミニポートの停止操作を処理する方法の詳細については、[仮想ミニポートを停止する](halting-a-virtual-miniport.md)を参照してください。

中間のドライバーを呼び出してから**NdisCloseAdapterEx**、そのバインドを適切なエラー状態のすべての送信要求が失敗する必要があります。

中間ドライバーのバインド解除操作の詳細については、[アダプターからバインド解除](unbinding-from-an-adapter.md)を参照してください。

 

 





