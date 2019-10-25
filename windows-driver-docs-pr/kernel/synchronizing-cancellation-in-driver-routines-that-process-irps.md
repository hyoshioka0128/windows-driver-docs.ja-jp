---
title: IRP を処理するドライバー ルーチン内でのキャンセルの同期
description: IRP を処理するドライバー ルーチン内でのキャンセルの同期
ms.assetid: 0b252ebd-b9d5-4747-9a27-c1ecffdbae18
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8818a41ef0831c9150362de9bc5e94defc856a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836187"
---
# <a name="synchronizing-cancellation-in-driver-routines-that-process-irps"></a>IRP を処理するドライバー ルーチン内でのキャンセルの同期





ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンなど、キャンセル可能な状態で保持されている IRP を使用してデキューまたは呼び出されたドライバールーチンは、次の操作を行う必要があります。

1.  [**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))を呼び出します。

2.  **Irp**が **&gt;DeviceObject**に等しいことを確認します。 それ以外の場合は、 [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出し、制御を返します。

    2つのが同じでない場合は、 [**Iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)がキャンセルスピンロックを解放し、このルーチンが取得した時刻の間に、存在していたものが取り消されて**いる可能性が**あります。

3.  **NULL**の*cancelルーチン*ポインターを使用して[**iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出し、キャンセル可能な状態から IRP を削除します。

4.  Irp をキャンセルするか、i/o 要求の処理を開始するかを決定するには、 **[irp-&gt;cancel** ] フィールドをオンにします。

    **[Irp&gt;Cancel]** が**TRUE**に設定されている場合は、次の手順を実行します。

    -   **IoReleaseCancelSpinLock**を呼び出します。
    -   **Irp&gt;iostatus に設定します。状態**は、\_取り消されました。
    -   **Irp-&gt;IoStatus. 情報**を0に設定します。
    -   [**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) ( *StartIo*ルーチン内) を呼び出して、次のパケットを開始します。
    -   I/O\_priority boost を使用して、IRP を完了するための\_インクリメントなしで[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

    **Irp&gt;Cancel**が**FALSE**に設定されている場合は、 **IoReleaseCancelSpinLock**を呼び出して、要求された i/o 要求の処理を開始するか、必要に応じて次の下位のドライバーに irp を渡します。

I/o マネージャーが提供するデバイスキューを使用するのではなく、独自の Irp のキューを管理するドライバーは、 **Iosetcancelroutine**を呼び出すときに、キャンセルスピンロックを取得する必要はありません。 ただし、これらのドライバーは、 **Iosetcancelroutine**が返す[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンポインターを確認して、キャンセルルーチンが既に開始されているかどうかを確認する必要があります。

取り消し可能な Irp を処理するドライバーでは、基になるデバイスの前に IRP を処理するすべてのドライバールーチンが、要求された i/o 操作に対してプログラムを実行するように、すべての受信 Irp の取り消し可能な状態をチェックする必要があります。 具体的には、 *StartIo*とコントローラーの両方の[*制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンがある最上位レベルのデバイスドライバーは、既に説明したように、両方のドライバールーチンで受信 irp を処理する必要があります。

 

 




