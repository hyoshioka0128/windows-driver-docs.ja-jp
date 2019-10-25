---
title: DMA 操作中のキャッシュ データのフラッシュ
description: DMA 操作中のキャッシュ データのフラッシュ
ms.assetid: 1b984b47-82cc-46b9-acad-73c5ed63e246
keywords:
- DMA 転送 WDK カーネル、データの整合性
- KeFlushIoBuffers
- FlushAdapterBuffers
- キャッシュされたデータのフラッシュ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13c78deaa9d36a428127c0077d5322daf5ba8ff0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836709"
---
# <a name="flushing-cached-data-during-dma-operations"></a>DMA 操作中のキャッシュ データのフラッシュ





一部のプラットフォームでは、プロセッサとシステム DMA コントローラー (またはバスマスタ DMA アダプター) がキャッシュの一貫性の異常を示しています。 次のガイドラインでは、DMA 操作インターフェイスのバージョン1または2を使用するドライバー ( [**dma\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)を参照) を有効にして、サポートされているすべてのプロセッサアーキテクチャで、キャッシュの一貫性を自動的に適用するハードウェア。

**注**  このトピックのガイドラインは、DMA 操作インターフェイスのバージョン1と2を使用するドライバーにのみ適用されます。 このインターフェイスのバージョン3を使用するドライバーは、異なる一連のガイドラインに従う必要があります。 詳細については、 [DMA 操作インターフェイスのバージョン 3](version-3-of-the-dma-operations-interface.md)を参照してください。

 

**DMA 操作中にデータの整合性を維持するために、最下位レベルのドライバーは次のガイドラインに従う必要があります。**

1.  プロセッサにキャッシュされる可能性のあるデータとメモリ内のデータの整合性を維持するために、転送操作を開始する前に[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)を呼び出します。

    ドライバーが、 *Cacheenabled*パラメーターを**TRUE**に設定して[**allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)を呼び出した場合、ドライバーは、バッファーからの転送操作を開始する前に**keflushiobuffers**を呼び出す必要があります。

2.  各デバイス転送操作の終了時に[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出して、システム DMA コントローラーのバッファーの残りのバイトがメモリまたは下位デバイスに書き込まれたことを確認します。

    または、特定の IRP に対する各転送操作の最後に、 **Flushadapterbuffers**を呼び出して、すべてのデータがシステムメモリに読み取られたか、バスマスタ DMA デバイスに書き込まれたことを確認します。

次の図は、ホストプロセッサと DMA コントローラーでキャッシュの一貫性が自動的に維持されない場合に、DMA を使用して、読み取りまたは書き込み操作を行う前にプロセッサキャッシュをフラッシュすることが重要である理由を示しています。

![dma を使用した読み取りおよび書き込み操作を示す図](images/16cchdma.png)

非同期の DMA 読み書き操作は、プロセッサキャッシュではなく、メモリ内のデータにアクセスします。 読み取りの直前に**Keflushiobuffers**を呼び出すことによってこのキャッシュがフラッシュされていない限り、後でプロセッサキャッシュをフラッシュすると、DMA 操作によってシステムメモリに転送されるデータが古いデータで上書きされる可能性があります。 書き込みの直前に**Keflushiobuffers**を呼び出すことによってプロセッサキャッシュがフラッシュされていない限り、このキャッシュ内のデータは、メモリ内のコピーよりも最新の状態になる可能性があります。

**Keflushiobuffers**は、プロセッサと DMA コントローラーがキャッシュの一貫性を維持するために依存している場合は何も行いません。そのため、このサポートルーチンを呼び出すと、このようなプラットフォームではほとんどオーバーヘッドが発生しません。

前の図にも示されているように、アダプターオブジェクトによって表される DMA コントローラーは内部バッファーを持つことができます。 このような DMA コントローラーは、固定サイズのチャンクでキャッシュされたデータを転送できます。通常は、8バイト以上のバイトです。 さらに、これらの DMA コントローラーは、各転送操作の前に内部バッファーがいっぱいになるまで待機できます。

下位 DMA を使用して、可変サイズのチャンクまたは固定サイズのチャンク (システム DMA コントローラーのキャッシュサイズの倍数ではない) のデータを読み取る最下位レベルのドライバーの場合を考えてみます。 このドライバーが各デバイスの転送の最後に**Flushadapterbuffers**を呼び出す場合を除き、ドライバーが要求したすべてのバイトが実際に転送されるかどうかを確認することはできません。

また、バスマスタ DMA デバイスのドライバーは、すべてのデータがシステムメモリまたはデバイスに転送されたことを確認するために、IRP の各転送操作の最後に**Flushadapterbuffers**を呼び出す必要があります。

**Flushadapterbuffers**は、要求されたフラッシュ操作が成功したかどうかを示すブール値を返します。 ドライバーは、この値を使用して、DMA の読み取りまたは書き込み操作に対して IRP を完了するときに i/o 状態ブロックを設定する方法を決定できます。

 

 




