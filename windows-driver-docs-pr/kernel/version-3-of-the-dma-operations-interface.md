---
title: DMA 操作インターフェイスのバージョン 3
description: DMA 操作インターフェイスのバージョン3は、Windows 8 以降で使用できます。
ms.assetid: EFB59930-7D58-4E6E-8242-66A326E239E5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ea19884b3289e43b2ccf7d131581b301b1867aab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835814"
---
# <a name="version-3-of-the-dma-operations-interface"></a>DMA 操作インターフェイスのバージョン 3


DMA 操作インターフェイスのバージョン3は、Windows 8 以降で使用できます。 このインターフェイスの**DMA\_操作**構造には、このインターフェイスの以前のバージョンで定義されていない多数の新しいルーチンが含まれています。 バージョン3のルーチンの一覧については、「 [**DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)」を参照してください。

DMA 操作インターフェイスのバージョン3は、すべての Windows ハードウェアプラットフォームで使用できますが、このインターフェイスには、カーネルモードドライバーがチップ (SoC) でシステムのシステム DMA コントローラーの高度な機能を使用できるようにするための機能が多数用意されています。接続. これらの機能には、通常、スキャッター/ギャザー DMA 転送を実行する機能が含まれています。 これに対し、以前のバージョンの DMA 操作インターフェイスでは、バスマスタ/ギャザー DMA 転送がバスマスタデバイスに制限されています。 バージョン3のインターフェイスを使用すると、スキャッター/ギャザーリストの管理が簡素化され、複雑な DMA 転送中のドライバーの介入の必要性が軽減されます。

Dma 操作インターフェイスのバージョン3を使用して DMA 転送を実行するには、通常、ドライバーは次のルーチンを呼び出します。

<a href="" id="iogetdmaadapter"></a>[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)  
Dma アダプターオブジェクトを割り当て、dma 操作インターフェイスを含む[**dma\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)構造体へのポインターを返します。

<a href="" id="getdmatransferinfo"></a>[**Getdmatransの情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_transfer_info)  
呼び出し元によって記述された DMA 転送を実行するために必要なリソースの説明を提供します。

<a href="" id="allocateadapterchannelex"></a>[**AllocateAdapterChannelEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex)  
DMA 転送に必要なリソースを割り当て、これらのリソースを DMA アダプターオブジェクトに割り当てます。

<a href="" id="maptransferex"></a>[**MapTransferEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)  
DMA 転送のマップレジスタとスキャッター/ギャザーバッファーを初期化し、転送を開始します。

<a href="" id="flushadapterbuffersex"></a>[**FlushAdapterBuffersEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex)  
DMA 転送の最後に必要になる可能性のあるキャッシュ操作を実行します。

<a href="" id="freeadapterchannel"></a>[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)  
DMA チャネルとマップレジスタを解放します。

<a href="" id="putdmaadapter"></a>[**PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter)  
アダプターオブジェクトを解放します。

これらのルーチンは、専用の DMA コントローラーを使用するバスマスタデバイスと、システム DMA コントローラーを共有する下位デバイスの両方で使用されます。 一般的な DMA 転送中にドライバーが行う呼び出しの詳細な説明については、「 [Version 3 Dma ルーチンの基本呼び出しパターン](basic-calling-pattern-for-version-3-dma-routines.md)」を参照してください。

**   dma**操作インターフェイスのバージョン3では、 [**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)ルーチンへの呼び出しは、dma 転送の前または後には必要ありません。 これは、次のルーチンが、ハードウェアにキャッシュの一貫性を適用しないプラットフォームでデータキャッシュをフラッシュする必要があるためです。

-   **Maptransferex**は、書き込み (メモリからデバイス) 転送の前にプロセッサデータキャッシュがフラッシュされることを保証します。
-   **Flushadapterbuffersex**は、読み取り (デバイスからメモリへの) 転送後にキャッシュが無効になることを保証します。

X86 または x64 プロセッサでは、 **Keflushiobuffers**の呼び出しで操作は実行されません。この呼び出しは、ハードウェアプラットフォームの動作に干渉することはありません。 ARM プロセッサでは、DMA 転送中に**Keflushiobuffers**を呼び出すと、不要なキャッシュ操作が実行され、パフォーマンスが低下する可能性があります。

 

 

 




