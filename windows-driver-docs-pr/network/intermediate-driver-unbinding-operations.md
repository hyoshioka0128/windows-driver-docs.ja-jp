---
title: 中間ドライバー バインド解除操作
description: 中間ドライバー バインド解除操作
ms.assetid: d316385a-9481-4708-9e09-06d0424acd8f
keywords:
- 中間ドライバー WDK ネットワーク、バインド
- NDIS 中間ドライバー WDK、バインド
- WDK NDIS 中間のバインド解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c30bc7ecc191d316d26f1b0fd593f10b2efc60c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844178"
---
# <a name="intermediate-driver-unbinding-operations"></a>中間ドライバー バインド解除操作





中間ドライバーは、 [*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数から[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)を呼び出すことによって、基になるミニポートドライバーからバインドを解除します。 基になるミニポートアダプターが使用できなくなった場合、NDIS は*Protocolunbindadapterex*を呼び出します。

ドライバーに[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)への未処理の呼び出しがある場合は、中間ドライバーの*Protocolunbindadapterex*関数が呼び出されることがあります。 この状況は、NDIS が、対応する仮想ミニポートを初期化するためにまだ[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出していない場合に発生します。 この場合、中間ドライバーは[**NdisIMCancelInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimcancelinitializedeviceinstance)を呼び出して、これらの仮想ミニポートの初期化をキャンセルしようとする必要があります。

閉じられているバインディングが中間ドライバーによってエクスポートされたデバイスにマップされ、そのデバイスが[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)を呼び出すことによって初期化された場合、中間ドライバーは[**NdisIMDeInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance)を呼び出してデバイスを閉じることができます。 その結果、中間ドライバーの仮想ミニポートは、上位レベルのドライバーによって行われた送信または要求に使用できなくなります。

NDIS 中間ドライバーが**NdisIMDeInitializeDeviceInstance**関数を呼び出すと、ndis は影響を受ける仮想ミニポートに対して[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 仮想ミニポートの停止操作の処理の詳細については、「[仮想ミニポートの停止](halting-a-virtual-miniport.md)」を参照してください。

中間ドライバーは**NdisCloseAdapterEx**を呼び出した後、適切なエラー状態を使用して、そのバインドに対するすべての送信要求を失敗させる必要があります。

中間ドライバーのバインド解除操作の詳細については、「[アダプターからのバインド](unbinding-from-an-adapter.md)解除」を参照してください。

 

 





