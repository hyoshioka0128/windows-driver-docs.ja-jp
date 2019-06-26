---
title: 中間ドライバー バインド解除操作
description: 中間ドライバー バインド解除操作
ms.assetid: d316385a-9481-4708-9e09-06d0424acd8f
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK, バインド
- バインド解除の WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e748cebdc37b238cb2997a6125db9cee2e1bf1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354549"
---
# <a name="intermediate-driver-unbinding-operations"></a>中間ドライバー バインド解除操作





中間のドライバーを呼び出すことによって、基になるミニポート ドライバーからバインド解除[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)からその[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数。 NDIS 呼び出し*ProtocolUnbindAdapterEx*場合は、基になるミニポート アダプターが使用できなくします。

中間のドライバーの*ProtocolUnbindAdapterEx*関数は、ドライバーに未処理の呼び出し時に呼び出される可能性があります[ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)します。 このような状況は、NDIS がまだ呼び出されていないときに発生します。 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)を対応する仮想 miniports を初期化します。 この場合、中間のドライバーを呼び出す必要があります[ **NdisIMCancelInitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimcancelinitializedeviceinstance)しようとすると、これらの仮想ミニポートの初期化をキャンセルします。

終了バインドは、中間のドライバーによってエクスポートされたデバイスにマップされている場合、そのデバイスは、呼び出すことによって初期化された場合[ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)、中間ドライバーを呼び出すことができます[ **NdisIMDeInitializeDeviceInstance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)デバイスを閉じます。 仮想ミニポートのドライバーの中間になりますまたはより高度なドライバーによって行われた要求の送信に使用できる不要になったことになります。

場合は、NDIS 中間ドライバの呼び出し、 **NdisIMDeInitializeDeviceInstance**関数では、NDIS 呼び出し、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)の影響を受ける仮想ミニポート関数. 仮想ミニポートの停止操作を処理する方法の詳細については、次を参照してください。[仮想ミニポートを停止する](halting-a-virtual-miniport.md)します。

中間のドライバーを呼び出してから**NdisCloseAdapterEx**、そのバインドを適切なエラー状態のすべての送信要求が失敗する必要があります。

中間ドライバーのバインド解除操作の詳細については、次を参照してください。[アダプターからバインド解除](unbinding-from-an-adapter.md)します。

 

 





