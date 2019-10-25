---
title: 共通バッファー DMA 用のシステム DMA コントローラーのセットアップ
description: 共通バッファー DMA 用のシステム DMA コントローラーのセットアップ
ms.assetid: 279776e0-dead-4763-9aae-33950837c27c
keywords:
- システム DMA WDK カーネル、共通バッファー
- 共通バッファー DMA WDK カーネル
- DMA 転送 WDK カーネル、共通バッファー
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65dea46b56f2b4177338d34768aff729d1c9098b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836341"
---
# <a name="setting-up-the-system-dma-controller-for-common-buffer-dma"></a>共通バッファー DMA 用のシステム DMA コントローラーのセットアップ





**Allocateadapterchannel**がドライバーの[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンに制御を転送する場合、ドライバーはシステム DMA コントローラーと一連のマップレジスタを "所有" します。 次に、ドライバーが転送操作用にデバイスを設定する前に、ドライバーが割り当てられた共通のバッファーを使用するようにシステム DMA コントローラーを設定するために、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)を呼び出す必要があります。

ドライバーは、 **Maptransfer**に次のパラメーターを提供します。

-   **IoGetDmaAdapter**によって返されるアダプターオブジェクトポインター

-   ドライバーによって割り当てられた共通バッファーを記述する MDL へのポインター

-   **Allocateadapterchannel**によってドライバーの*adaptercontrol*ルーチンに渡された*mapregisterbase*ハンドル

-   ドライバーによって割り当てられた共通バッファーのサイズ (バイト単位) を示す変数 (*長さ*) へのポインター

-   転送操作の方向を示すブール値 (システムメモリからデバイスへの要求された転送の場合は TRUE)

**Maptransfer**は論理アドレスを返します。システム DMA を使用するドライバーは無視する必要があります。 **Maptransfer**が制御を返す場合、ドライバーは DMA 操作用にデバイスを設定する必要があります。 ドライバーは**Maptransfer**を1回だけ呼び出しますが、要求された転送が完了するまで、共通バッファーとロックダウンされたユーザーバッファーの間でデータのコピーを続けます。

ドライバーは[**ReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)を呼び出して、現在、共通バッファーで転送されているバイト数を確認できます。ドライバーは、DMA 操作の方向に応じて、ユーザーデータを使用して共通バッファーにデータを格納したり、共通バッファーからユーザーバッファーにデータをコピーしたりすることができます。

転送が完了するか、ドライバーが IRP のエラー状態を返す必要がある場合、ドライバーは[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出して、システム DMA コントローラーにキャッシュされているすべてのデータがシステムメモリに読み込まれるか、デバイスに書き込まれるようにします。 次に、ドライバーは、任意のドライバー (それ自体を含む) で使用するために、 [**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)をすぐに呼び出して、システム DMA コントローラーを解放する必要があります。

 

 




