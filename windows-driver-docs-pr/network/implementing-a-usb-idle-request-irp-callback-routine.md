---
title: USB アイドル状態の要求の IRP のコールバック ルーチンを実装します。
description: USB アイドル状態の要求の IRP のコールバック ルーチンを実装します。
ms.assetid: B3F843CD-E9D8-4ABD-9BC9-08C5AB7CDB98
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6670eb750287ea1937b883aca2554066302734
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539326"
---
# <a name="implementing-a-usb-idle-request-irp-callback-routine"></a>USB アイドル状態の要求の IRP のコールバック ルーチンを実装します。


ときに[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)を呼び出すと、USB のミニポート ドライバー呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) I/O 要求パケット (IRP) を発行するにはUSB のアイドル状態の要求 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) に、基になる USB バス ドライバー。 ミニポート ドライバーでは、ネットワーク アダプターがアイドル状態し、中断する必要があります、USB バス ドライバーに通知するには、この IRP を発行します。

USB ミニポート ドライバーでは、USB アイドル要求 IRP の IRP のコールバック ルーチンを提供する必要があります。 USB バス ドライバーは、ネットワーク アダプターの中断し、低電力状態に移行することを確認するときに、このルーチンを呼び出します。

**注**  後に、USB バス ドライバーが IRP USB アイドル状態要求を処理、いずれかへの呼び出しのコンテキストで同期的に、コールバック ルーチンを呼び出します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または後で非同期的に[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)を返します。

 

呼び出すコールバック ルーチンがしか[ **NdisMIdleNotificationConfirm** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)ネットワーク アダプターの省電力状態の遷移を続行できる NDIS を通知するためにします。 ドライバーを呼び出すと**NdisMIdleNotificationConfirm**、ネットワーク アダプターに移行できる、最も低いデバイスの電源状態も指定する必要があります。

呼び出しのコンテキスト内で[ **NdisMIdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/hh451492)NDIS 低電力状態にネットワーク アダプターに移行するために必要な手順を実行します。 詳細については、[、NDIS セレクティブ サスペンド アイドル状態の通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)を参照してください。

次は、USB アイドル要求 IRP のコールバック ルーチンの例です。

```C++
//
// MiniportUsbIdleRequestCallback()
//
// This is the USB selective suspend idle notification.  All that is 
// needed is to inform NDIS that the USB stack is ready to go to a 
// low-power state.  Be aware that USB devices will always be requested
// to transition to a power state of NdisDeviceStateD2.
//
VOID MiniportUsbIdleRequestCallback(PVOID AdapterContext)
{
    NdisMIdleNotificationConfirm(
        AdapterContext->MiniportAdapterHandle,
        NdisDeviceStateD2
        );

    return;
}
```

USB のアイドル状態の要求のコールバック ルーチンの詳細については、USB アイドル要求 IRP のコールバック ルーチンを参照してください。

 

 





