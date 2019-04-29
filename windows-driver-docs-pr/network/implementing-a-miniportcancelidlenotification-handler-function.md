---
title: MiniportCancelIdleNotification ハンドラー関数の実装
description: MiniportCancelIdleNotification ハンドラー関数の実装
ms.assetid: 51C25573-5723-44F9-B498-EBEF6756F3B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7f94031ba27898a11dd9fcf2ba3fca0d3a65541
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383648"
---
# <a name="implementing-a-miniportcancelidlenotification-handler-function"></a>MiniportCancelIdleNotification ハンドラー関数の実装


NDIS ミニポート ドライバーの呼び出す[ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)アイドル状態の通知プロセスをキャンセルし、ネットワーク アダプターに電力状態に移行するためにハンドラー関数。 この関数が呼び出されたときに、ミニポート ドライバーは次の手順に従います。

1.  ミニポート ドライバーでは、アイドル状態の通知で以前発行がある可能性があります bus 固有 Irp を取り消す必要があります。

2.  ミニポート ドライバー呼び出し[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)します。 この呼び出しでは、アイドル状態の通知が完了したこと、NDIS に通知します。 NDIS し、選択的複雑、ネットワーク アダプターを電力状態に遷移することによって操作を中断します。

たとえば、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)を呼び出すと、USB のミニポート ドライバー呼び出し[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338) I/O をキャンセルするにはUSB のアイドル状態の要求の要求パケット (IRP) ([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)). USB のミニポート ドライバーでは、この IRP で以前発行されたその[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数。 USB バス ドライバーが IRP をキャンセルするとすぐに IRP の完了ルーチンを呼び出します。 USB バス ドライバー完了ルーチンを呼び出すと IRP は取り消され、デバイスが電力状態に再開できることを確認します。 ミニポート ドライバーが呼び出し完了ルーチンのコンテキストで[ **NdisMIdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/hh451491)します。

**注**  USB バス ドライバー呼び出すことができます完了ルーチンの呼び出しのコンテキストで同期的に[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)または後に非同期的に[*MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)を返します。

 

例を次に、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088) USB ミニポート ドライバーのハンドラー関数。 この例では、USB アイドル要求 IRP のキャンセルに関連する手順を示します。

```C++
//
// MiniportCancelIdleNotification()
//
// This routine is called if NDIS has to cancel an idle notification.
// All that is needed is to cancel the selective suspend IRP.
//
VOID MiniportCancelIdleNotification(
    _In_ NDIS_HANDLE MiniportAdapterContext
    )
{
    IoCancelIrp(Adapter->UsbSsIrp);
}
```

USB アイドル要求 IRP の完了ルーチンの実装のガイドラインについては、次を参照してください。 [USB のアイドル状態要求 IRP の完了ルーチンを実装する](implementing-a-usb-idle-request-irp-completion-routine.md)します。

 

 





