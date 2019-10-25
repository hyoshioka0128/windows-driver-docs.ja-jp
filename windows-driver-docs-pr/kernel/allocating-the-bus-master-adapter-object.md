---
title: バス マスター アダプター オブジェクトの割り当て
description: バス マスター アダプター オブジェクトの割り当て
ms.assetid: fc80d3f8-a12e-40bd-8b0e-c6bca2f9e7de
keywords:
- バスマスターアダプターオブジェクトの割り当て
- バスマスタ DMA WDK カーネル
- DMA 転送 WDK カーネル、バスマスタ DMA
- アダプタオブジェクト WDK カーネル、バスマスタ DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bda0d6be05a99bfe51738b8f0f4cde446a4dbd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837227"
---
# <a name="allocating-the-bus-master-adapter-object"></a>バス マスター アダプター オブジェクトの割り当て





パケットベースのバスマスタ DMA を準備するために、ドライバーは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)の受信後に[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)と[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出します。 ドライバーがこれらのルーチンを呼び出すためには、そのディスパッチルーチンが IRP のパラメーターの有効性を確認する必要があります。 さらに処理するために、IRP を別のドライバールーチンにキューに追加することもできます。 転送要求は、デバイス i/o 操作を必要とする現在の IRP です。

**Allocateadapterchannel**を呼び出すドライバールーチンは、IRQL = DISPATCH\_レベルで実行されている必要があります。 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返されるアダプターオブジェクトへのポインターと共に、ドライバーは、 **Allocateadapterchannel**を呼び出すときに次のものを提供する必要があります。

-   現在の IRP のターゲットデバイスオブジェクトへのポインター

-   [*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンのエントリポイント

-   *アダプターコントロール*ルーチンが使用するドライバーによって決定されたコンテキスト情報へのポインター

**Allocateadapterchannel**は、ドライバーの*adaptercontrol*ルーチンをキューに配置します。このルーチンは、アダプターオブジェクトが解放され、ターゲットデバイスとの間でドライバーの DMA 操作に一連の[マップレジスタ](map-registers.md)が割り当てられている場合に実行されます。

入力時に、 *Adaptercontrol*ルーチンには、割り当てられたマップレジスタのハンドル (*mapregisterbase*) に加えて、 **allocateadapterchannel**への呼び出しで渡された*DeviceObject*および*コンテキスト*ポインターが付与されます。

また、ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合、 *adaptercontrol*ルーチンには **&gt;DeviceObject**を指すポインターが付与されます。 ドライバーが*StartIo*ルーチンではなく irp の独自のキューを管理している場合、ドライバーは、 **Allocateadapterchannel**を呼び出すときに渡されるコンテキストの一部として、現在の irp へのポインターを含める必要があります。

スキャッター/ギャザー機能のないバスマスタ DMA デバイスのドライバーでは、 *Adaptercontrol*ルーチンは通常、次のことを行います。

1.  ドライバーが DMA 操作に関して保持するすべてのコンテキストを保存または初期化します。 このコンテキストには、ドライバーが[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)および[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)に渡す必要がある入力*MAPREGISTERBASE*ハンドル、IRP 内の i/o スタック位置からの要求された転送の**長さ**(バイト単位) などがあります。

2.  デバイスが転送操作を開始するために使用できる論理アドレスを取得するために、 [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)の後に**maptransfer** (次の「[転送操作の設定](setting-up-a-transfer-operation.md)」で説明) を呼び出します。

3.  バスマスターアダプターを設定して、転送操作を開始します。

4.  値**DeallocateObjectKeepRegisters**を返します。

スキャッター/ギャザー機能を備えたバスマスタデバイスのドライバーでは、 *Adaptercontrol*ルーチンは通常、次のことを行います。

1.  ドライバーが処理する DMA 操作に関するすべての状態を保存または初期化します。これには、ドライバーが**Maptransfer**および**flushadapterbuffers**に渡す必要がある*mapregisterbase*ハンドルの保存、要求の**長さ**(バイト単位)IRP 内の i/o スタックの場所から転送します。

2.  **Mmgetmdlvirtualaddress**の後に**maptransfer** (次のサブセクションで説明します) を呼び出して、デバイスが転送操作を開始するために使用できる論理アドレスを取得します。

    *Adaptercontrol*ルーチンは、使用可能なすべてのマップレジスタを使用して、バスマスターアダプターのスキャッター/ギャザーリストを構築するまで、maptransfer を繰り返し呼び出します。

3.  バスマスターアダプターを設定して、転送操作を開始します。

4.  値**DeallocateObjectKeepRegisters**を返します。

詳細については、「 [AdapterControl ルーチンの記述](writing-adaptercontrol-routines.md)」を参照してください。

バスマスタ DMA を実行するドライバーは、デバイスでスキャッター/ギャザー DMA がサポートされているかどうかに関係なく、 [**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)ルーチンと[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)ルーチンを使用できます。 これらのルーチンを使用すると、ドライバーの*Adaptercontrol*ルーチンの要件が変更されます。詳細については、「[スキャッター/GATHER DMA の使用](using-scatter-gather-dma.md)」を参照してください。

*Adaptercontrol*ルーチンは、IO\_割り当て\_アクション型のシステム定義値を返す必要があります。 バスマスタ DMA を使用するドライバーの場合、 *Adaptercontrol*ルーチンは通常、値**DeallocateObjectKeepRegisters**を返す必要があります。これにより、ドライバーは、ターゲットデバイスオブジェクトに割り当てられたマップレジスタを保持できます。現在の IRP に対して要求されたすべてのデータを転送しました。 転送が完了したら、DPC ルーチンは[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)を呼び出して、割り当てられたマップレジスタを解放する必要があります。 ただし、デバイスがコマンドキューをサポートしていない場合、現在の IRP の転送が完了すると、 *Adaptercontrol*ルーチンは**KeepObject**を返すことができ、DPC ルーチンは代わりに[**freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)を呼び出すことができます。

*Adaptercontrol*ルーチンは、バスマスターアダプターが DMA 操作を完了するまで待機することはできません。

バスマスタアダプターでスキャッター/ギャザーがサポートされているかどうかに関係なく、 *Adaptercontrol*ルーチンは少なくとも次の操作を行う必要があります。

1.  必要なコンテキスト情報 (特に*Mapregisterbase*ハンドル) を、ドライバーのデバイス拡張機能、コントローラー拡張機能、またはドライバーがアクセス可能なその他の常駐ストレージ領域 (ドライバーによって割り当てられた非ページプール) に保存します。 ドライバーは、 **Maptransfer**および**flushadapterbuffers**を呼び出すときに、このハンドルに渡す必要があります。

2.  **DeallocateObjectKeepRegisters**を返します。

各 DMA 転送操作が完了すると、別のドライバールーチン (通常は[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチン) が**flushadapterbuffers**を呼び出す必要があります。 また、このルーチンでは、現在の IRP を満たすために必要な追加の DMA 操作も設定する必要があります。

ドライバーが現在の IRP の転送要求を満たしているか、デバイスまたはバス i/o エラーが原因で IRP を失敗させる必要がある場合は、 **FreeMapRegisters**を呼び出す必要があります。 この呼び出しは、現在の IRP に対する**Flushadapterbuffers**の最後の呼び出しの直後に発生する必要があります。これにより、ドライバーは他の DMA 要求 (場合によってはバス上の他のデバイス) にサービスを実行できるようになります。

 

 




