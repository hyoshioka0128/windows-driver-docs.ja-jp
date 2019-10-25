---
title: DPC ルーチンの記述
description: DPC ルーチンの記述
ms.assetid: a0b93b71-7ee3-4626-b0b8-5dd6e19fba0d
keywords:
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cef336b8f7c71520e31ed801186dca6bd5df5515
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835566"
---
# <a name="writing-dpc-routines"></a>DPC ルーチンの記述





[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)と[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンの主な役割は、次のデバイス i/o 操作がすぐに開始され、現在の IRP を完了することを保証することです。

*DpcForIsr*または*customdpc*ルーチンによって実行されるその他の作業は、ドライバーの設計とデバイスの性質によって異なります。 たとえば、 *DpcForIsr*または*customdpc*ルーチンは、次のいずれかを実行することもできます。

-   タイムアウトまたは失敗した操作を再試行してください。

-   [**Ioallocateerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)を呼び出し、デバイス i/o エラーを報告するエラーログパケットを設定して、 [**iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)を呼び出します。

    I/o エラーの処理の詳細については、「[エラーのログ記録](logging-errors.md)」を参照してください。

-   ドライバーで[バッファー i/o](methods-for-accessing-data-buffers.md)が使用されている場合、または irp がデバイス制御操作を指定している場合は、irp を完了する前に、デバイスから irp **-&gt;AssociatedIrp**のシステムバッファーに読み込まれたデータを転送します。

-   ドライバーが[直接 i/o](methods-for-accessing-data-buffers.md)を使用し、大規模な転送を小さい断片に分割する必要がある場合は、完了した部分転送操作ごとに状態を保存し、次の部分転送の範囲を計算して、ドライバーによって提供される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)を使用します。次の部分転送操作のためにデバイスをプログラミングするルーチン。

    バッファーされた i/o を使用するドライバーでも、デバイスの転送機能が制限されている場合は、転送要求を分割する必要があります。

-   ドライバーでパケットベースの DMA が使用されている場合は、各デバイスの転送操作の後に[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出し、部分的な転送のシーケンスが完了し、完全転送要求が実行されたときに[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)または[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)を呼び出します。満たさ.

    要求された転送が、1つの DMA 操作で一部しか満たされない場合、通常、 *DpcForIsr*または*customdpc*ルーチンは、IRP の指定したバイト数が完全に転送されるまで、1つ以上の dma 操作を設定します。

    DMA の使用方法の詳細については、「[アダプターオブジェクトと dma](adapter-objects-and-dma.md)」を参照してください。

-   ドライバーがプログラミング i/o (PIO) を使用している場合は、現在の IRP が読み取りを要求した場合、各転送操作の最後に[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)を呼び出します。

    要求された転送が、1つの PIO 操作で一部しか満たされない場合、通常、 *DpcForIsr*または*customdpc*ルーチンは、IRP の指定されたバイト数が完全になるまで、1つ以上の転送操作を設定します。支払.

    PIO の使用方法の詳細については、「 [Direct i/o の使用](using-direct-i-o.md)」を参照してください。

-   WDM 以外のドライバーに[*コントローラー制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンがある場合は、要求された操作が完了したら[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)を呼び出します。

通常、 *DpcForIsr*または*customdpc*ルーチンでは、ほとんどのドライバーのデバイス i/o 処理が irp を満たしていることに注意してください。 また、これらのルーチンは、ドライバーのディスパッチルーチンを使用して、Irp をデバイスにキューに置いている役割を担います。

一般的な設計ガイドラインを次に示します。

-   *DpcForIsr*または*customdpc*ルーチンは、この呼び出しを安全に行うことができるようになるとすぐに[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出す必要があります。これは、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンまたはを使用してリソースの競合や競合状態が発生する可能性はありません。*StartIo*ルーチンによって実行されるその他のルーチン。

-   ドライバーが Irp のキューを独自に管理している場合、その*DpcForIsr*または*customdpc*ルーチンは、次の irp をデキューし、次の要求のためにデバイスを設定するのが安全であるとすぐに、ドライバーに通知する必要があります。

*DpcForIsr*または*Customdpc*ルーチンは**iostartnextpacket**を呼び出す必要があります。それ以外の場合は、次の要求のデバイス i/o 処理を開始できるときに適切なドライバールーチンに通知します。 ドライバーとそのデバイスによっては、 *DpcForIsr*または*Customdpc*ルーチンが[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)で現在の irp を完了する前に問題が発生したり、このルーチンが現在の irp を完了する直前に発生したりすることがあります。コントロールを返します。

 

 




