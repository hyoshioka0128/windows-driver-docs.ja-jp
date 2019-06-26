---
title: StartIo ルーチンを使用しているドライバーのキャンセル ルーチン
description: StartIo ルーチンを使用しているドライバーのキャンセル ルーチン
ms.assetid: 5098e4b9-d4db-44c2-acb3-a46878d6f1c4
keywords:
- Irp、StartIo ルーチンのキャンセル
- キャンセル ルーチン、StartIo ルーチン
- StartIo ルーチン、キャンセル ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 857a3b4bceb1fb95e8fc4d31cbbdc97686daecf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385119"
---
# <a name="cancel-routines-in-drivers-with-startio-routines"></a>StartIo ルーチンを使用しているドライバーのキャンセル ルーチン





I/O マネージャーが保持、 **CurrentIrp**フィールドに関連付けられているデバイスのキュー オブジェクトの Irp がキューに置かれた場合にのみ、デバイス オブジェクト。 フィールドが、ドライバーがある場合にのみ有効です。 つまり、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。

持つドライバーでは、 *StartIo*ルーチン、一般的な[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンは、次を実行する必要があります。

1.  入力 IRP のポインターがターゲット デバイス オブジェクトのと一致するかどうか確認**CurrentIrp**アドレス。

    これらのポインターが等しい場合、*キャンセル*ルーチンの呼び出し[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を渡して、 **Irp-&gt;CancelIrql**、コントロールを返します。

2.  取り消された IRP が現在の IRP ではない場合は、入力の取り消された IRP がデバイスのキューを呼び出すことによって、ターゲット デバイス オブジェクトに関連付けられているかどうかを確認[ **KeRemoveEntryDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremoveentrydevicequeue) IRP のに**Tail.Overlay.DeviceQueueEntry**ポインター。
    -   IRP がデバイスのキューにある場合は、呼び出す**KeRemoveEntryDeviceQueue**キューから削除されます。 *キャンセル*ルーチンの呼び出し[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))、ステータスの IRP の I/O の状態のブロック設定\_の中止された**の状態**の場合は 0 と**情報**、呼び出し[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)キャンセルの IRP とコントロールを返します。

    -   デバイスのキューに IRP がない場合、*キャンセル*ルーチンの呼び出し**IoReleaseCancelSpinLock**と制御が戻ります。

ドライバーの*キャンセル*ルーチンを呼び出す必要があります**KeRemoveEntryDeviceQueue** IRP がデバイスのキューであるかどうかをテストします。 このサポート ルーチンは、特定の IRP をデバイスのキューから削除しますか返す以外は何も**FALSE**、指定したエントリがキューがないことを示します。 A*キャンセル*ルーチンでは、呼び出すことができないために、入力の IRP がデバイスのキュー内の任意の特定位置にあるがあると想定ことはできません[ **KeRemoveDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue)または[**KeRemoveByKeyDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovebykeydevicequeue) IRP が返されるへのポインターを比較し、IRP を入力します。

ドライバーを*キャンセル*ルーチンが処理できる[ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)も要求します。 参照してください[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)の詳細については**IRP\_MJ\_クリーンアップ**要求。

 

 




