---
title: パケットベース DMA 用のアダプター チャネルの割り当て
description: パケットベース DMA 用のアダプター チャネルの割り当て
ms.assetid: c95e4b2d-ce19-453a-bcc5-4bb37fc5d9ed
keywords:
- システム DMA WDK カーネル、パケットベース
- パケットベースの DMA WDK カーネル
- DMA 転送 WDK カーネル、パケットベース
- アダプターチャネルの割り当て
- アダプターチャネル割り当て WDK カーネル
- AllocateAdapterChannel
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c18215fa31c5d7add7f583bff6dfb8056c09b75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837231"
---
# <a name="allocating-an-adapter-channel-for-packet-based-dma"></a>パケットベース DMA 用のアダプター チャネルの割り当て





パケットベースのシステム DMA を準備するために、ドライバーは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求を受信した後に[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)と[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出します。

ドライバーがこれらのルーチンを呼び出す前に、 [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン (または DMA 転送を処理するその他のディスパッチルーチン) が IRP のパラメーターの有効性を確認している必要があります。 ディスパッチルーチンは、他の処理のために別のドライバールーチンに対して IRP をキューに入れている場合もあります。

**Allocateadapterchannel**を呼び出すドライバールーチンは、IRQL = DISPATCH\_レベルで実行されている必要があります。 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返されるアダプターオブジェクトへのポインターと共に、ドライバーは、 **Allocateadapterchannel**を呼び出すときに次のものを提供する必要があります。

-   ターゲットデバイスオブジェクトへのポインター

-   [*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンのエントリポイント

-   *アダプターコントロール*ルーチンが使用するドライバーによって決定されたコンテキスト情報へのポインター

**Allocateadapterchannel**は、ドライバーの*adaptercontrol*ルーチンをキューに配置します。このルーチンは、システム dma コントローラーがこのドライバーに割り当てられ、ドライバーの DMA 操作に[マップレジスタ](map-registers.md)のセットが割り当てられたときに実行されます。

エントリでは、 *Adaptercontrol*ルーチンは、割り当てられたマップレジスタのハンドル (*mapregisterbase*) に加えて、 **allocateadapterchannel**への呼び出しで渡される*DeviceObject*および*コンテキスト*ポインターを受け取ります。

また、ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合、 *adaptercontrol*ルーチンは **&gt;DeviceObject**へのポインターも受け取ります。 ドライバーが Irp の独自のキューを管理している場合 ( *StartIo*ルーチンを持つのではなく)、ドライバーは、 **Allocateadapterchannel**を呼び出すときに渡されるコンテキストの一部として、現在の irp へのポインターを含める必要があります。

*Adaptercontrol*ルーチンは、通常、次のことを行います。

1.  ドライバーが DMA 操作に関して保持するすべてのコンテキストを保存または初期化します。 このコンテキストには、ドライバーが[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)および[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)に渡す必要がある入力*mapregisterbase*ハンドルと、要求された転送の**長さ**が IRP 内の i/o スタックの場所から渡される可能性があります。

2.  [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)の後に**maptransfer**を呼び出します。 「[パケットベースの dma 用のシステム Dma コントローラーの](setting-up-the-system-dma-controller-for-packet-based-dma.md)セットアップ」を参照してください。

3.  転送操作を開始するための下位デバイスを設定します。

4.  値**KeepObject**を返します。

すべての*Adaptercontrol*ルーチンは、型[**IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)のシステム定義値を返す必要があります。 システム DMA を使用するドライバーの場合、 *Adaptercontrol*ルーチンは値**KeepObject**を返す必要があります。 これにより、ドライバーは、要求されたすべてのデータを転送するまで、システム DMA コントローラーの "所有権" を保持し、割り当てられたマップレジスタを保持することができます。

*アダプターコントロール*ルーチンは、下位デバイスが DMA 操作を実行するのを待機することはできないため、各*adaptercontrol*ルーチンは、少なくとも次の操作を行う必要があります。

1.  コンテキスト情報、特に*Mapregisterbase*ハンドルを、ドライバーのデバイス拡張機能、コントローラー拡張機能、またはその他のドライバーがアクセス可能な常駐ストレージ領域 (ドライバーによって割り当てられた非ページプール) に保存します。

2.  **KeepObject**を返します。

詳細については、「 [AdapterControl ルーチンの記述](writing-adaptercontrol-routines.md)」を参照してください。

各 DMA 転送操作が完了すると、別のドライバールーチン (通常は[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチン) が[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出す必要があります。 また、このルーチンは、現在の IRP の転送要求を満たすために DMA コントローラーを複数回設定する必要がある場合に、 **Maptransfer**と**flushadapterbuffers**を再度呼び出す必要があります。

ドライバーが現在の IRP の要求を満たしている場合は、 [**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)を呼び出す必要があります。 このサポートルーチンは、現在の IRP に対する**Flushadapterbuffers**への最後の呼び出しの直後に呼び出されます。これにより、システムの DMA コントローラーを (任意のドライバーによって) 使用できるようになり、他の転送要求の迅速を満たすことができるようになります。

スキャッター/ギャザー機能を持つ下位デバイスのドライバーも、その*Adaptercontrol*ルーチンから**KeepObject**を返す必要があります。 ドライバーが特定の DMA 要求を分割する必要があるときに、システム DMA コントローラーが DMA 操作間で再プログラミングされている間、デバイスは待機できる必要があります。 一部の Windows プラットフォームでは、このようなデバイスは、1つのマップレジスタだけをそのデバイスのドライバーに割り当てることができるため、DMA 操作ごとのデータページをほとんど転送できます。

 

 




