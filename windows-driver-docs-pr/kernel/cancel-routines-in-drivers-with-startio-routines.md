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
ms.openlocfilehash: 3ba91d7266f9a04dd6ba57b9c98ea28bb042d406
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338551"
---
# <a name="cancel-routines-in-drivers-with-startio-routines"></a>StartIo ルーチンを使用しているドライバーのキャンセル ルーチン





I/O マネージャーが保持、 **CurrentIrp**フィールドに関連付けられているデバイスのキュー オブジェクトの Irp がキューに置かれた場合にのみ、デバイス オブジェクト。 フィールドが、ドライバーがある場合にのみ有効です。 つまり、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。

持つドライバーでは、 *StartIo*ルーチン、一般的な[*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)ルーチンは、次を実行する必要があります。

1.  入力 IRP のポインターがターゲット デバイス オブジェクトのと一致するかどうか確認**CurrentIrp**アドレス。

    これらのポインターが等しい場合、*キャンセル*ルーチンの呼び出し[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)を渡して、 **Irp-&gt;CancelIrql**、コントロールを返します。

2.  取り消された IRP が現在の IRP ではない場合は、入力の取り消された IRP がデバイスのキューを呼び出すことによって、ターゲット デバイス オブジェクトに関連付けられているかどうかを確認[ **KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163) IRP のに**Tail.Overlay.DeviceQueueEntry**ポインター。
    -   IRP がデバイスのキューにある場合は、呼び出す**KeRemoveEntryDeviceQueue**キューから削除されます。 *キャンセル*ルーチンの呼び出し[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)、ステータスの IRP の I/O の状態のブロック設定\_の中止された**の状態**の場合は 0 と**情報**、呼び出し[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)キャンセルの IRP とコントロールを返します。

    -   デバイスのキューに IRP がない場合、*キャンセル*ルーチンの呼び出し**IoReleaseCancelSpinLock**と制御が戻ります。

ドライバーの*キャンセル*ルーチンを呼び出す必要があります**KeRemoveEntryDeviceQueue** IRP がデバイスのキューであるかどうかをテストします。 このサポート ルーチンは、特定の IRP をデバイスのキューから削除しますか返す以外は何も**FALSE**、指定したエントリがキューがないことを示します。 A*キャンセル*ルーチンでは、呼び出すことができないために、入力の IRP がデバイスのキュー内の任意の特定位置にあるがあると想定ことはできません[ **KeRemoveDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553156)または[**KeRemoveByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553152) IRP が返されるへのポインターを比較し、IRP を入力します。

ドライバーを*キャンセル*ルーチンが処理できる[ **IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)も要求します。 参照してください[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)の詳細については**IRP\_MJ\_クリーンアップ**要求。

 

 




