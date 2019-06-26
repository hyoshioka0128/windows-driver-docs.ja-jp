---
title: DMA 操作中のキャッシュ データのフラッシュ
description: DMA 操作中のキャッシュ データのフラッシュ
ms.assetid: 1b984b47-82cc-46b9-acad-73c5ed63e246
keywords:
- DMA は、WDK カーネルでは、データの整合性を転送します。
- KeFlushIoBuffers
- FlushAdapterBuffers
- キャッシュされたデータのフラッシュ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee326a8f5df5ed787a0e1e55be193b010c77b9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386593"
---
# <a name="flushing-cached-data-during-dma-operations"></a>DMA 操作中のキャッシュ データのフラッシュ





一部のプラットフォームで、プロセッサおよび DMA コント ローラーのシステム上 (または各バス マスター DMA アダプター) キャッシュ コヒレンシー異常が発生します。 次のガイドラインは、バージョン 1 または 2 の DMA 操作のインターフェイスを使用するドライバーを有効にする (を参照してください[ **DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)) サポートされているすべてのプロセッサ全体で一貫性のあるキャッシュの状態を維持するにはこのアーキテクチャでは、自動的にキャッシュの一貫性を強制するハードウェアを含まないアーキテクチャを含むです。

**注**  DMA 操作のインターフェイスのバージョン 1 および 2 を使用するドライバーにのみ、このトピックのガイドラインが適用されます。 このインターフェイスのバージョン 3 を使用するドライバーは、異なる一連のガイドラインに従う必要があります。 詳細については、次を参照してください。 [DMA 操作のインターフェイスのバージョン 3](version-3-of-the-dma-operations-interface.md)します。

 

**DMA 操作中にデータの整合性を維持するために最下位レベルのドライバーに次のガイドラインに従います**

1.  呼び出す[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)プロセッサでキャッシュされる可能性がデータとメモリ内のデータ間の一貫性を維持するために、転送操作を開始する前にします。

    ドライバーを呼び出す場合[ **AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer)で、 *CacheEnabled*パラメーターに設定**TRUE**ドライバーはを呼び出す必要があります**KeFlushIoBuffers**と、バッファーからの転送操作を開始する前にします。

2.  呼び出す[ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)各デバイスの転送操作の最後に必ずシステム DMA コント ローラーのバッファーの残りの部分 (バイト) が書き込まれたメモリにまたは下位のデバイスにします。

    か、または、 **FlushAdapterBuffers**特定の IRP の各転送操作の最後に必ずすべてのデータ システム メモリに読み込まれるまたはされたバス マスター DMA のデバイスに書き込まれます。

プロセッサをフラッシュする重要な理由は次の図に示すは、読み取り前にキャッシュまたはホスト プロセッサと DMA コント ローラー、自動的に保持しないキャッシュの一貫性がある場合は、DMA を使用して操作を記述します。

![dma を使用して操作を読み書き説明する図](images/16cchdma.png)

非同期の DMA は、読み取りまたは書き込み操作のデータにアクセスのメモリ内で、プロセッサのキャッシュではなく。 呼び出すことによって、このキャッシュがフラッシュされた場合を除き、 **KeFlushIoBuffers**直前に、読み取り、DMA 操作をシステム メモリに転送されるデータでしたデータで上書きする古くなった後に、プロセッサのキャッシュをフラッシュする場合。 呼び出すことによって、プロセッサのキャッシュがフラッシュされた場合を除き、 **KeFlushIoBuffers**書き込みで直前に、このキャッシュ内のデータが、メモリ内のコピーより最新可能性があります。

**KeFlushIoBuffers**は何もに、プロセッサおよび DMA コント ローラーを使用する場合は、キャッシュの一貫性を維持、ためこのサポート ルーチンを呼び出し、このようなプラットフォームでオーバーヘッドはほとんどありません。

として前の図のようにも、アダプター オブジェクトで表される、DMA コント ローラーは、内部バッファーを持つことができます。 DMA コント ローラーには、一度に通常 8 個以上のバイト、固定サイズのチャンク単位でキャッシュされたデータを転送できます。 さらに、これらの DMA コント ローラーは、内部バッファーが各転送操作の前にいっぱいになるまで待機できます。

可変サイズのチャンクまたはシステム DMA コント ローラーのキャッシュ サイズの整数倍ではない固定サイズのチャンク単位でデータを読み取る下位 DMA を使用する最下位レベルのドライバーの場合を考えます。 このドライバーを呼び出さない限り、 **FlushAdapterBuffers**デバイスの各転送の末尾にはすることはできないことを確認してときに、ドライバーが要求された実際に転送されるすべてのバイト数。

バス マスター DMA のデバイスのドライバーも呼び出す必要があります**FlushAdapterBuffers** IRP をシステム メモリにすべてのデータが転送されたことを確認するには、各転送操作の最後に、またはデバイスにします。

**FlushAdapterBuffers**要求のフラッシュ操作が成功したかどうかを示すブール値、値を返します。 ドライバーは、読み取りまたは書き込み操作の DMA IRP の完了時に、状態の I/O ブロックを設定するのに方法については、この値を使用できます。

 

 




