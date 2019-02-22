---
title: USB アイドル状態の要求の IRP の完了ルーチンを実装します。
description: USB アイドル状態の要求の IRP の完了ルーチンを実装します。
ms.assetid: C9435A1D-031B-4F67-B968-66534C48A9BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7786be1cc3108e0135e1c026e1cc4742eb0ab5c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549192"
---
# <a name="implementing-a-usb-idle-request-irp-completion-routine"></a>USB アイドル状態の要求の IRP の完了ルーチンを実装します。


ときに[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)を呼び出すと、USB のミニポート ドライバー呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) I/O 要求パケット (IRP) を発行するにはUSB のアイドル状態の要求 ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) に、基になる USB バス ドライバー。 ミニポート ドライバーでは、ネットワーク アダプターがアイドル状態し、中断する必要があります、USB バス ドライバーに通知するには、この IRP を発行します。

USB のミニポート ドライバーに呼び出す必要がありますも[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686) USB アイドル要求 IRP の完了ルーチンを登録するためにします。 USB バス ドライバーは、USB のミニポート ドライバーによって取り消される後 IRP が完了すると、完了ルーチンを呼び出します。 NDIS は呼び出すことによって、アイドル状態の通知をキャンセルすると、USB のミニポート ドライバーは IRP をキャンセル[ *MiniportCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464088)します。

呼び出して完了ルーチンがしか[ **NdisMIdleNotificationComplete** ](https://msdn.microsoft.com/library/windows/hardware/hh451492)ネットワーク アダプターの電力状態の遷移を続行できる NDIS を通知するためにします。

**注**  完了ルーチンの状態を返す必要があります\_詳細\_処理\_USB ミニポート ドライバーが IRP のリソースを再利用 NDIS から別のアイドル状態通知中にかどうかに必要な。

 

次は、USB アイドル要求 IRP の完了ルーチンの例です。

```C++
//
// MiniportUsbIdleRequestCompletion()
//
// This is the IO_COMPLETION_ROUTINE for the selective suspend IOCTL.
// All that is needed is to inform NDIS that the IdleNotification
// operation is complete.
//
VOID MiniportUsbIdleRequestCompletion(PVOID AdapterContext)
{
    NdisMIdleNotificationComplete(Adapter->MiniportAdapterHandle);

    // We will be reusing the IRP later, so do not let the IO manager delete it.
    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

USB のアイドル状態の要求のコールバック ルーチンの詳細については、USB アイドル要求 IRP の完了ルーチンを参照してください。

 

 





