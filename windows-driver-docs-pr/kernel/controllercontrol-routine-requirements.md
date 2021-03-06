---
title: ControllerControl ルーチンの要件
description: ControllerControl ルーチンの要件
ms.assetid: b311c0b0-f7b1-4276-a165-5c658657b198
keywords:
- コント ローラー オブジェクトの WDK カーネル、ControllerControl ルーチンを記述
- 書き込みの ControllerControl ルーチン
- ControllerControl ルーチン、要件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1e76d9d27587e802f918ff4830d90846d3f98a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377218"
---
# <a name="controllercontrol-routine-requirements"></a>ControllerControl ルーチンの要件





その名のとおり、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンは、コント ローラー オブジェクトに関連付けします。 ときに、 *ControllerControl*ルーチンの実行、コント ローラーのオブジェクトによって表されるハードウェアは無料、およびコント ローラー拡張機能一般にアクセスしていない別のドライバー ルーチンによってしない限り、コント ローラー拡張機能ドライバーの ISR. と共有されているコンテキストが含まれています

通常、 *ControllerControl*ルーチンは次の処理には少なくとも。

1.  更新プログラムまたはドライバーには、ターゲット デバイス オブジェクトの拡張機能でデバイスとコント ローラー拡張機能でどのようなコンテキストを初期化します

    ドライバーは、DMA を使用している場合、 *ControllerControl*ルーチンは通常かどうかを特定の転送要求する必要がありますに分割するシステムによるいずれかが原因の部分的な転送または上のデバイスによる制限を判断する責任を負いますが、DMA の各転送のサイズ。 このような場合、 *ControllerControl*ルーチンも呼び出し元の責任は[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)ドライバーがある場合、 *AdapterControl*ルーチン。

    ドライバーが PIO を使用している場合、 *ControllerControl*ルーチンもは責任を負います[転送要求を分割](splitting-dma-transfer-requests.md)と呼び出し元の転送部分範囲にすると、そのハードウェア プログラムが、必要な場合、 [**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で MDL で**Irp -&gt;MdlAddress**します。

2.  要求された I/O 操作に対して、ハードウェアをプログラムします。

    デバイスまたはコント ローラーの拡張機能は、ISR からアクセスできる場合、 *ControllerControl*ルーチンを使用する必要があります、 [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)呼び出すことによって呼び出されるルーチン[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)します。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

ドライバーがある場合、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンでは、その*ControllerControl*ルーチンも確認する必要があります、 **Irp -&gt;キャンセル**フィールド現在の IRP が取り消す必要があるし、次のいずれかの操作を行うかどうかを判断するには。

場合**Irp -&gt;キャンセル**に設定されている**TRUE**、 *ControllerControl*ルーチンは、次を実行する必要があります。

1.  状態を設定\_の中止された**状態**の場合は 0 と**情報**IRP の I/O の状態のブロックにします。

2.  呼び出す[ **IoFreeController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller) [次へ] のデバイス操作をすぐに開始できるように、コント ローラー オブジェクトを解放します。

3.  呼び出す[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)またはドライバーが、独自のキューを管理する場合、[次へ] の IRP をデキューします。

4.  取り消された IRP の完了[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)コントロールを返します。

場合**Irp -&gt;キャンセル**に設定されていない**TRUE**、 *ControllerControl*ルーチンは代わりに、次を実行する必要があります。

1.  呼び出す[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)をリセットする、*キャンセル*に IRP の日常的なエントリ ポイント**NULL**します。 ドライバーは、デバイス オブジェクトで I/O マネージャーが指定したデバイスのキューを使用する場合は、この呼び出しの [キャンセル] スピン ロックを取得します。

2.  プログラムで、要求された I/O 操作のハードウェアを使用して、 [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンの呼び出しによって呼び出される[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution). 詳細については、次を参照してください[クリティカル セクションを使用する。](using-critical-sections.md)

キャンセル可能な Irp の処理の詳細については、次を参照してください。[キャンセル Irp](canceling-irps.md)します。

オーバー ラップ処理を物理コント ローラー/アダプターにアタッチされているさまざまなデバイスでの I/O 操作を除く最も割り込み駆動、 *ControllerControl*ルーチンを返す必要があります**KeepObject**[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチンでは、操作と IRP が完了するとします。

IRP を完了するルーチンを呼び出す必要がありますを現在の要求を満たすために I/O 操作が完了したら、すぐ**IoFreeController**と**います**できるように、次の要求できる限り迅速に処理されます。

場合、 *ControllerControl*ルーチン自体は IRP を完了するか、ディスク シークなどの操作を設定できる場合の 1 つのターゲット デバイス オブジェクト (ディスク) をでしたと重ねることが、操作をもう 1 つのデバイス オブジェクト、 *ControllerControl*ルーチンを返す必要があります**DeallocateObject**します。

 

 




