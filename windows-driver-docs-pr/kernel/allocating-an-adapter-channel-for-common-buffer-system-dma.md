---
title: 共通バッファー システム DMA 用のアダプター チャネルの割り当て
description: 共通バッファー システム DMA 用のアダプター チャネルの割り当て
ms.assetid: 3b426b5e-e555-458c-8e16-0d59a7cb9bd6
keywords:
- アダプターチャネルの割り当て
- アダプターチャネル割り当て WDK カーネル
- AllocateAdapterChannel
- システム DMA WDK カーネル、共通バッファー
- 共通バッファー DMA WDK カーネル
- DMA 転送 WDK カーネル、共通バッファー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03e0ba87c32a9998458fb7d0410575942b25ef1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828664"
---
# <a name="allocating-an-adapter-channel-for-common-buffer-system-dma"></a>共通バッファー システム DMA 用のアダプター チャネルの割り当て





ドライバーは、 [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン (または DMA 転送を処理するその他のディスパッチルーチン) の実行後に[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出して、irp のパラメーターが有効かどうかを確認します。これは、場合によっては1つ以上の irp をキューに入れます。さらに処理するための別のドライバールーチン。必要に応じて、転送されるデータと共に共通のバッファーが読み込まれる場合があります。

**Allocateadapterchannel**を呼び出すドライバールーチンは、IRQL = DISPATCH\_レベルで実行されている必要があります。 **Allocateadapterchannel**ルーチンは、ドライバーの[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンをキューに配置します。このルーチンは、システム dma コントローラーがこのドライバーに割り当てられた後に実行され、一連の[マップレジスタ](map-registers.md)がドライバーの DMA 操作に割り当てられています。

入力時に、 *Adaptercontrol*ルーチンには、割り当てられたマップレジスタのハンドルだけでなく、 **Allocateadapterchannel**への呼び出しで渡されたデバイスオブジェクトとコンテキストへのポインターが渡されます。 また、ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合、 *adaptercontrol*ルーチンには **&gt;DeviceObject**を指すポインターが付与されます。 ドライバーが*StartIo*ルーチンではなく irp の独自のキューを管理している場合、ドライバーは、 **Allocateadapterchannel**を呼び出すときに渡されるコンテキストデータの一部として、現在の irp へのポインターを含める必要があります。

*Adaptercontrol*ルーチンは、通常、次のことを行います。

1.  ドライバーが DMA 操作に関して保持するすべてのコンテキストを保存または初期化します。 このコンテキストには、ドライバーが[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)および[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)に渡す必要がある入力*mapregisterbase*ハンドルと、要求された転送の**長さ**が IRP 内の i/o スタックの場所から渡される可能性があります。

2.  転送操作を開始するための下位デバイスを設定します。

3.  値**KeepObject**を返します。

詳細については、「 [AdapterControl ルーチンの記述](writing-adaptercontrol-routines.md)」を参照してください。

システム DMA コントローラーの自動初期化モードを使用するドライバーの場合、 *Adaptercontrol*ルーチンは値**KeepObject**を返す必要があります。 これにより、ドライバーは、すべてのデータが転送されるまで、システム DMA コントローラーと割り当てられたマップレジスタの "所有権" を保持することができます。

*アダプターコントロール*ルーチンは、下位デバイスが DMA 操作を実行するのを待機することはできないため、 *adaptercontrol*ルーチンは少なくとも次の操作を行う必要があります。

1.  コンテキスト情報、特に*Mapregisterbase*ハンドルを、ドライバーのデバイス拡張機能、コントローラー拡張機能、またはその他のドライバーがアクセス可能な常駐ストレージ領域 (ドライバーによって割り当てられた非ページプール) に保存します。

2.  **KeepObject**を返します。

DMA 転送操作の完了時に、別のドライバールーチン ( [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンなど) が[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)と[**freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)を呼び出す必要があります。

 

 




