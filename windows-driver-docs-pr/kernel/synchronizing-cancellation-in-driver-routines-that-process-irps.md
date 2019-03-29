---
title: IRP を処理するドライバー ルーチン内でのキャンセルの同期
description: IRP を処理するドライバー ルーチン内でのキャンセルの同期
ms.assetid: 0b252ebd-b9d5-4747-9a27-c1ecffdbae18
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f51e1689195247afe2e554249a2ad94d8d462790
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569930"
---
# <a name="synchronizing-cancellation-in-driver-routines-that-process-irps"></a>IRP を処理するドライバー ルーチン内でのキャンセルの同期





デキューまたはドライバーを含む、キャンセル可能な状態に保持されている IRP が呼び出された任意のドライバー ルーチン[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンでは、次を実行する必要があります。

1.  呼び出す[ **IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)します。

2.  確認します**Irp** equals**デバイス オブジェクト -&gt;CurrentIrp**します。 そうでない場合は、呼び出す[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)コントロールを返します。

    2 つが同じ場合、 **CurrentIrp**までの時間がキャンセルされたを[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)キャンセル スピン ロックとこのルーチンを獲得してリリースします。

3.  呼び出す[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)で、 **NULL** *CancelRoutine* IRP をキャンセル可能な状態から削除へのポインター。

4.  チェック、 **Irp -&gt;キャンセル**IRP をキャンセルするか、I/O 要求の処理を開始するかを判断するフィールド。

    場合**Irp -&gt;キャンセル**に設定されている**TRUE**次の操作を行います。

    -   呼び出す**IoReleaseCancelSpinLock**します。
    -   設定**Irp -&gt;IoStatus.Status**ステータス\_キャンセルします。
    -   設定**Irp -&gt;IoStatus.Information**を 0 にします。
    -   呼び出す[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358) (で、 *StartIo*ルーチン) を次のパケットを開始します。
    -   呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IO の優先順位を上げると\_いいえ\_IRP の完了をインクリメントします。

    場合**Irp -&gt;キャンセル**に設定されている**FALSE**、呼び出す**IoReleaseCancelSpinLock**要求の処理、I/O 要求を開始したり、[次へ] の下に、IRP を渡す適切なドライバーです。

I/O マネージャーが指定したデバイスのキューを使用するのではなく、Irp の独自のキューを管理するドライバーを呼び出すときに、キャンセル スピン ロックを取得する必要はありません**IoSetCancelRoutine**します。 ただし、これらのドライバーを確認する必要があります、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)日常的なポインターを**IoSetCancelRoutine**キャンセル ルーチンが既に開始されているかどうかを判断するを返します。

キャンセル可能な Irp を処理するすべてのドライバー、IRP を基になるデバイスが要求された I/O 操作の設定前に処理するすべてのドライバーのルーチンはすべての着信 Irp のキャンセル可能な状態を確認する必要があります。 両方の最上位レベルのデバイス ドライバー具体的には、 *StartIo*と[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンでこれらの 2 つのドライバー ルーチンとして受信 Irp を処理する必要があります既に説明しています。

 

 




