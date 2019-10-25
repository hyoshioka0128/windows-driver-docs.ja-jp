---
title: ControllerControl ルーチンの要件
description: ControllerControl ルーチンの要件
ms.assetid: b311c0b0-f7b1-4276-a165-5c658657b198
keywords:
- コントローラーオブジェクト WDK カーネル、コントローラー制御ルーチンの記述
- コントローラー制御ルーチン、書き込み
- コントローラーコントロールルーチン、要件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 019bd8497b7378b20f704a6388ee9adebcfb54a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837045"
---
# <a name="controllercontrol-routine-requirements"></a>ControllerControl ルーチンの要件





名前が示すように、コントローラーオブジェクトには、コントローラーの[*制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンが関連付けられています。 コントローラーの*制御*ルーチンが実行されると、コントローラーオブジェクトによって表されるハードウェアは解放され、コントローラーの拡張機能には、というコンテキストが含まれていない限り、通常は別のドライバールーチンによってアクセスされません。ドライバーの ISR と共有します。

通常、*コントローラー制御*ルーチンは、少なくとも次のものを実行します。

1.  ターゲットデバイスオブジェクトとコントローラー拡張機能のデバイス拡張機能でドライバーによって保持されるコンテキストを更新または初期化します。

    ドライバーが DMA を使用する場合、通常*は、各*dma 転送のサイズに対してシステムによる制限またはデバイスによる制限により、特定の転送要求を部分的な転送に分割する必要があるかどうかを判断します. このような状況では、ドライバーに*Adaptercontrol*ルーチンがある場合は、*コントローラー制御*ルーチンも[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出す必要があります。

    ドライバーで PIO が使用されている場合は、その*コントローラーのコントローラー*が、[転送要求](splitting-dma-transfer-requests.md)(ハードウェアが必要な場合) を部分転送範囲内に分割し、MDL を使用して[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出すことができます。**Irp-&gt;MdlAddress**。

2.  要求された i/o 操作のハードウェアをプログラムします

    ISR からデバイスまたはコントローラーの拡張機能にアクセスできる*場合は、* [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出すことによって呼び出される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを使用する必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

ドライバーに[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが含まれている場合は、その*コントローラーのコントローラーの制御*ルーチンも、現在の irp をキャンセルする必要があるかどうかを判断し、次のいずれかの操作を実行するために、 **irp&gt;cancel**フィールドを確認する必要があります。

**Irp&gt;Cancel**が**TRUE**に設定されている場合、*コントローラー制御*ルーチンは次の操作を行う必要があります。

1.  状態に対して [状態] **\_[キャンセル] を設定**し、IRP の i/o 状態ブロックの**情報**を0に設定します。

2.  [**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)を呼び出してコントローラーオブジェクトを解放し、次のデバイス操作をすぐに開始できるようにします。

3.  [**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出すか、ドライバーが独自のキューを管理する場合は次の IRP をデキューします。

4.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)と return コントロールを使用して、取り消された IRP を完了します。

**Irp&gt;Cancel**が**TRUE**に設定されていない場合、代わりに、*コントローラー制御*ルーチンは次の操作を行う必要があります。

1.  [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出して、IRP の*キャンセル*ルーチンのエントリポイントを**NULL**にリセットします。 ドライバーがデバイスオブジェクトで i/o マネージャーによって指定されたデバイスキューを使用する場合は、この呼び出しのキャンセルスピンロックを取得します。

2.  [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出すことによって呼び出される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを使用して、要求された i/o 操作のハードウェアをプログラムします。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

キャンセル可能な Irp の処理の詳細については、「 [irp の取り消し](canceling-irps.md)」を参照してください。

物理コントローラー/アダプターに接続されている異なるデバイスでのオーバーラップ操作を除き、ほとんどの割り込みドリブン i/o 操作では、 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または [*KeepObject が原因で、コントローラーコントロールルーチンは、CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、操作と IRP を完了します。

現在の要求を満たす i/o 操作が完了するとすぐに、IRP を完了するルーチンは、次の要求を可能な限り迅速に処理できるように、 **IoFreeController**と**Iostartnextpacket**を呼び出す必要があります。

*コントローラーコントロール*ルーチン自体が IRP を完了した場合、または別のデバイスオブジェクトの操作とオーバーラップする可能性のある1つのターゲットデバイスオブジェクト (ディスク) に対して、ディスクシークなどの操作を設定できる場合は、*コントローラー制御*ルーチン**Deallocateobject**を返す必要があります。

 

 




