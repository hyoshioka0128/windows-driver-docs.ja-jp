---
title: 共通バッファーシステム DMA の使用
description: 共通バッファーシステム DMA の使用
ms.assetid: ee060aa4-2db4-4bd2-b107-b71acced97fd
keywords:
- システム DMA WDK カーネル、共通バッファー
- 共通バッファー DMA WDK カーネル
- DMA 転送 WDK カーネル、共通バッファー
- AllocateCommonBuffer
- 自動初期化モード WDK DMA
- 連続 DMA WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936cd28acd52d74121b4afcaacaf8b00afb9e951
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838371"
---
# <a name="using-common-buffer-system-dma"></a>共通バッファーシステム DMA の使用





システム DMA コントローラーの自動初期化モードを使用するドライバーは、DMA 転送を実行できるバッファーにメモリを割り当てる必要があります。このバッファーを取得するために、ドライバーは[**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)を呼び出します。通常は、IRP\_を処理し、 [ **\_デバイス要求を開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理する[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからです。 次の図は、ドライバーがバッファーを割り当て、その仮想アドレス範囲をシステムの物理メモリにマップする方法を示しています。

![ドライバーがシステム dma に共通のバッファーを割り当てる方法を示す図](images/3hlsysbf.png)

前の図に示すように、ドライバーは次の手順を実行してシステム DMA 用のバッファーを割り当てます。

1.  ドライバーは[**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)を呼び出し、 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返されたアダプターオブジェクトへのポインターと、バッファーに要求されたバイト単位の長さを渡します。 メモリを経済的に使用するには、バッファーの入力*長*値がページ\_サイズ以下であるか、またはページ\_サイズの整数倍数である必要があります。

2.  **Allocatecommonbuffer**が**NULL**ポインターを返す場合、ドライバーは、既に要求されているシステムリソースを解放し、状態を返します。 IRP\_の\_の開始に応じて、リソース\_不足し\_リソースが不足し **\_デバイス**要求。

    それ以外の場合、 **Allocatecommonbuffer**は、システム仮想アドレス空間に要求された量のメモリを割り当て、そのバッファーへの2つの異なる種類のポインターを返します。

    -   ドライバーがストレージを提供する必要がありますが、それ以降は無視する必要があるバッファーの*logicaladdress* (前の図の bufferlogicaladdress)

    -   バッファーの仮想アドレス (前の図では BufferVirtualAddress)。ドライバーも格納する必要があります。これにより、DMA 操作用のバッファーを記述する MDL を作成できるようになります。

    ドライバーは、これらのポインターをデバイス拡張機能またはその他のドライバーによって割り当てられた常駐メモリに格納する必要があります。

3.  ドライバーは[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を呼び出して、バッファーに MDL を割り当てます。 ドライバーは、 **Allocatecommonbuffer**によって返されたバッファーの*virtualaddress*とそのバッファーの*長さ*を渡して、MDL を割り当てます。

4.  ドライバーは、 **IoAllocateMdl**によって返されたポインターを使用して[**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)を呼び出し、常駐バッファーの仮想アドレス範囲をシステムの物理メモリにマップします。

共通バッファーを割り当て、その仮想アドレス範囲をマップした後、下位デバイスのドライバーは、DMA 転送を要求する IRP の処理を開始できます。 これを行うために、ドライバーは次の一般的な一連のサポートルーチンを呼び出します。

1.  ドライバーの作成者の裁量で、 [**RtlMoveMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlmovememory)は、ロックダウンされたユーザーバッファーから、デバイスへの転送用にドライバーで割り当てられた共通バッファーにデータをコピーします。

2.  ドライバーが DMA 用にデバイスをプログラミングする準備ができていて、システム DMA コントローラーが必要な場合の**Allocateadapterchannel**

3.  転送操作用にシステム DMA コントローラーを設定するために、ドライバーによって割り当てられた共通バッファーを記述する MDL を使用した[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)

    ドライバーが**Maptransfer**を1回呼び出すだけで、その共通のバッファーを使用するようにシステム DMA コントローラーが設定されることに注意してください。 転送中、ドライバーは[**ReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)を呼び出して、転送されるバイト数を確認できます。また、必要に応じて、 **RtlMoveMemory**を呼び出して、ユーザーバッファーとの間でデータをコピーします。

4.  ドライバーが下位デバイスとの間で DMA 転送を完了したときの[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)

5.  要求されたすべてのデータが転送されるか、またはデバイス i/o エラーが原因でドライバーが IRP を失敗させる必要がある場合、すぐに[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 。

**IoGetDmaAdapter**によって返されるアダプターオブジェクトのポインターは、 **RtlMoveMemory**以外の各サポートルーチンに必須のパラメーターです。

個々のドライバーは、各ドライバーがどのように実装されているかに応じて、さまざまな時点でこの一連のサポートルーチンを呼び出します。 たとえば、1つのドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが**Allocateadapterchannel**を呼び出す可能性があります。別のドライバーは、ドライバーによって作成されたインタロックされたキューから irp を削除するルーチンからこの呼び出しを行う可能性がありますが、別のドライバーがこれを行う可能性があります。データ転送の準備ができていることを下位 DMA デバイスが示している場合は、を呼び出します。

 

 




