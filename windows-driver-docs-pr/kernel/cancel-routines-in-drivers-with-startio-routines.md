---
title: StartIo ルーチンを使用しているドライバーのキャンセル ルーチン
description: StartIo ルーチンを使用しているドライバーのキャンセル ルーチン
ms.assetid: 5098e4b9-d4db-44c2-acb3-a46878d6f1c4
keywords:
- Irp の取り消し、StartIo ルーチン
- Cancel ルーチン、StartIo ルーチン
- StartIo ルーチン、キャンセルルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41238c0b966ec396e0b3c037b30deb45369ff8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837116"
---
# <a name="cancel-routines-in-drivers-with-startio-routines"></a>StartIo ルーチンを使用しているドライバーのキャンセル ルーチン





I/o マネージャーは、関連付けられたデバイスキューオブジェクトで Irp がキューに置かれている場合にのみ、デバイスオブジェクト**の "状態**" フィールドを保持します。 つまり、このフィールドは、ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合にのみ有効です。

*StartIo*ルーチンがあるドライバーでは、一般的な[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンは次の操作を行う必要があります。

1.  入力された IRP のポインターがターゲットデバイスオブジェクトの '% **Entirp** ' アドレスと一致するかどうかを確認します。

    これらのポインターが等しい場合、*キャンセル*ルーチンは[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出し、 **Irp-&gt;cancelirql**を渡して、制御を返します。

2.  取り消された IRP が現在の IRP ではない場合は、IRP の**末尾のオーバーレイ**を使用して[**Keremoveentrydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)を呼び出し、ターゲットデバイスオブジェクトに関連付けられているデバイスキューに、入力が取り消されたことがあるかどうかを確認します。
    -   IRP がデバイスキューにある場合、 **Keremoveentrydevicequeue**を呼び出すと、キューから削除されます。 *キャンセル*ルーチンは、 [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出し、IRP の i/o 状態ブロック**を状態に対して**キャンセルし、**情報**を0に設定し、キャンセルされた irp を使用して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、状態を\_します。コントロールを返します。

    -   IRP がデバイスキューに存在しない場合、*キャンセル*ルーチンは**IoReleaseCancelSpinLock**を呼び出し、制御を返します。

ドライバーの*キャンセル*ルーチンは、IRP がデバイスキューにあるかどうかをテストするために**Keremoveentrydevicequeue**を呼び出す必要があります。 このサポートルーチンは、指定された IRP をデバイスキューから削除するか、 **FALSE**を返す以外は何も行いません。これは、指定されたエントリがキューに登録されていないことを示します。 *キャンセル*ルーチンでは、入力 irp がデバイスキュー内の特定の位置にあると想定できません。そのため、 [**keremovedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)または[**keremovebykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue)を呼び出して、返された irp と入力 irp とのポインターを比較することはできません。

*キャンセル*ルーチンが含まれているドライバーは、 [**IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)要求も処理できます。 **IRP\_MJ\_クリーンアップ**要求の詳細については、「 [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 」を参照してください。

 

 




