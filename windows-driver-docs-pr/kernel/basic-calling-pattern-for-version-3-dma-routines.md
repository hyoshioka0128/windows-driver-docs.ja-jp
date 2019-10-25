---
title: バージョン 3 の DMA ルーチンの基本的な呼び出しパターン
description: DMA 操作インターフェイスのバージョン3でルーチンを使用する DMA 転送を実行するには、ドライバーが次の一覧に記載されている手順に従う必要があります。
ms.assetid: 5D73120F-79F5-4C9A-8AE5-25D5CF9B06F5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 42c17f53e7bea4d3d7db1df4f483ec7d0f7f010f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828627"
---
# <a name="basic-calling-pattern-for-version-3-dma-routines"></a>バージョン 3 の DMA ルーチンの基本的な呼び出しパターン


DMA 操作インターフェイスのバージョン3でルーチンを使用する DMA 転送を実行するには、ドライバーが次の一覧に記載されている手順に従う必要があります。 これらの手順は、下位デバイスとバスマスタデバイスの両方に共通です。 このインターフェイスのバージョン3は、Windows 8 以降で使用できます。 このインターフェイスのルーチンの詳細については、「 [**DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)」を参照してください。

## <a name="step-1-obtain-a-dma-adapter-object"></a>手順 1: DMA アダプターオブジェクトを取得する


DMA 転送の準備として、ドライバーは[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)ルーチンを呼び出して、dma アダプターオブジェクトを取得します。 DMA アダプターオブジェクトは、システムの DMA コントローラーのバスマスタデバイスまたは要求行を表すソフトウェアオブジェクトです。 このオブジェクトには、デバイスとの間でデータを転送するために使用されるバスの DMA 操作インターフェイスが含まれています。 さらに、このオブジェクトは、転送を実行するために必要な共有リソースへのドライバーのアクセスを同期します。 詳細については、「[アダプターオブジェクトの概要](introduction-to-adapter-objects.md)」を参照してください。

## <a name="step-2-obtain-a-description-of-the-required-dma-resources"></a>手順 2: 必要な DMA リソースの説明を取得する


ドライバーは、 [**Getdmatransferinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_transfer_info)ルーチンを呼び出して、転送を実行するために必要な DMA リソースの説明を取得します。

この呼び出しの入力パラメーターは、転送に使用するメモリバッファーと転送の方向 (読み取りまたは書き込み) を示します。

この呼び出しから取得されるリソース要件には、マップレジスタの数と、転送のデータバッファーを記述するために必要なスキャッター/ギャザーリストのサイズが含まれます。 後続の[**Allocateadapterchannelex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex)ルーチンの呼び出し ([手順 3](#step-3-request-the-required-dma-resources)を参照) では、ドライバーは map レジスタ count を入力パラメーターとして提供します。

## <a name="step-3-request-the-required-dma-resources"></a>手順 3: 必要な DMA リソースを要求する


ドライバーは、割り当てられたリソースを割り当てて DMA アダプターオブジェクトに割り当てるために、 [**Allocateadapterchannelex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel_ex)ルーチンを呼び出します。 これらのリソースには、DMA チャネルとマップレジスタが含まれます。

**Allocateadapterchannelex**の呼び出しは、非同期または同期にすることができます。

DMA\_同期\_コールバックフラグが設定されていない場合、呼び出しは非同期です。 この場合、 *Executionroutine*パラメーターは、要求されたリソースが使用可能になったときに呼び出される呼び出し元によって提供される実行ルーチンを指します。 成功した場合、非同期**Allocateadapterchannelex**呼び出しによって、実行ルーチンが実行されるのを待たずに STATUS\_SUCCESS が返されます。

DMA\_同期\_コールバックフラグが設定されている場合、 **Allocateadapterchannelex**の呼び出しは同期です。 この場合、呼び出しの*Executionroutine*パラメーターは省略可能であり、 **Allocateadapterchannelex**は次のように動作します。

-   *Executionroutine*が NULL 以外で、DMA リソースをすぐに割り当てることができる場合、 **Allocateadapterchannelex**は呼び出し元スレッドのコンテキストで実行ルーチンを呼び出します。 実行ルーチンの実行が完了すると、 **Allocateadapterchannelex**から STATUS\_SUCCESS が返されます。 リソースがすぐに利用できない場合、 **Allocateadapterchannelex**は失敗し、エラー状態コードの状態を返します。リソース\_不足して\_ます。

-   *Executionroutine*が NULL で、 **ALLOCATEADAPTERCHANNELEX**が DMA リソースをすぐに割り当てることができる場合、 **ALLOCATEADAPTERCHANNELEX**はステータス\_SUCCESS を返します。 すべてのリソースがすぐに利用できない場合、呼び出しは失敗し、エラー状態コードの状態\_\_リソースが不足します。

STATUS\_SUCCESS を返す同期呼び出しの場合、 **allocateadapterchannelex**への*mapregisterbase*パラメーターが NULL 以外の場合、 **allocateadapterchannelex**は、割り当てられたマップのベースアドレスをに書き込みます。*Mapregisterbase*パラメーターが指すアドレス。 *Executionroutine*が null の場合、 *mapregisterbase*は null 以外である必要があります。 *Executionroutine*が NULL 以外の場合、 **Allocateadapterchannelex**への*mapregisterbase*パラメーターは省略可能であり、実行ルーチンはマップレジスタのベースアドレスを入力パラメーターとして受け取ります。

非同期**Allocateadapterchannelex**呼び出しの場合、 *EXECUTIONROUTINE*は NULL 以外にする必要があり、実行ルーチンはマップレジスタのベースアドレスを入力パラメーターとして受け取ります。

後続の[**Maptransferex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)ルーチンの呼び出し ([手順 5](#step-5-initialize-the-dma-resources-and-start-the-dma-transfer)を参照) では、ドライバーはマップレジスタのベースアドレスを入力パラメーターとして提供します。

*Executionroutine*が NULL 以外の場合、実行ルーチンは、割り当てられたリソースのディスポジションを示す状態値を返します。 システム DMA 転送の場合、この戻り値は**KeepObject**である必要があります。 この値は、アダプターオブジェクト (および割り当てられているすべてのリソース) が使用中であり、解放されてはならないことをオペレーティングシステムに通知します。 実行ルーチンが指定されていない場合、ドライバーは代わりに[**Freeadapterobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_object)ルーチンを呼び出し、 **KeepObject**を割り当て*オプション*パラメーターとして指定する必要があります。

## <a name="step-4-if-necessary-cancel-the-pending-resource-request"></a>手順 4: 必要に応じて、保留中のリソース要求をキャンセルする


**Allocateadapterchannelex**呼び出しによって dma リソースを待機する dma アダプターがキューにある場合、ドライバーは必要に応じて[**canceladapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pcancel_adapter_channel)ルーチンを呼び出して、保留中のリソース要求をキャンセルできます。

**Canceladapterchannel**が TRUE を返した場合、リソース要求は正常にキャンセルされます。 実行ルーチンが**Allocateadapterchannelex**呼び出しで指定されている場合、このルーチンは実行されません。

**Canceladapterchannel**が FALSE を返す場合、リソース要求は既に許可されているため、取り消すことはできません。 実行ルーチンが**Allocateadapterchannelex**呼び出しで指定されている場合、このルーチンが呼び出されます。

## <a name="step-5-initialize-the-dma-resources-and-start-the-dma-transfer"></a>手順 5: DMA リソースを初期化し、DMA 転送を開始する


このドライバーは、DMA リソースを初期化し、DMA 転送を開始するために、 [**Maptransferex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)を呼び出します。 この呼び出しは、 **Allocateadapterchannelex**を呼び出す同じドライバースレッドで発生する場合があります。または、ドライバーが**allocateadapterchannelex**に提供する実行ルーチンで発生する可能性があります。 DMA データバッファー全体を転送するために複数の**Maptransferex**呼び出しが必要な場合、前の**maptransferex**呼び出しの完了ルーチンで、後の**maptransferex**呼び出しが発生する可能性があります。

**Maptransferex**では、入力パラメーターとしてチェーン mdls がサポートされています。 各 MDL は、仮想メモリ内で連続している DMA バッファーの領域を記述します。 **Maptransferex**によってスキャッター/ギャザーリストが構築されると、事実上連続するバッファー領域から次のように、ドライバーの介入なしに自動的に遷移が処理されます。 詳細については、「 [MapTransferEx ルーチンの使用](using-the-maptransferex-routine.md)」を参照してください。

システム DMA 転送の場合、オプションの*Dmacompletionroutine*パラメーターで、dma 完了ルーチンへのポインターを**maptransferex**に渡すことができます。 このルーチンは、DMA 転送が完了したことを示すシステム DMA コントローラーからの割り込みに応答して、ディスパッチレベルで実行するようにスケジュールされています。

**Maptransferex**が要求された転送サイズ全体をマップできない場合は、\**長さ*の出力パラメーターをマップされた長さに設定し、STATUS\_SUCCESS を返します。

## <a name="step-6-if-necessary-perform-hardware-specific-operations"></a>手順 6: 必要に応じて、ハードウェア固有の操作を実行する


**Maptransferex**は、DMA 転送が正常に開始されたことを示す状態\_SUCCESS を返します。 プラットフォームによっては、転送を開始するために、 **Maptransferex**の呼び出し以外に、追加のアクションを実行することが必要になる場合がありますが、この種の遅延開始はすべてのプラットフォームで必要になるわけではありません。 ドライバーは、割り当てられたリソースの使用および解放に関する決定の遅延に依存しないようにする必要があります。

DMA 操作インターフェイスのルーチンは、これらのルーチンを使用するドライバーに対して透過的な方法で、DMA 転送のキャッシュの一貫性を維持します。 ハードウェアにキャッシュの一貫性を適用しないプラットフォームでは、 **Maptransferex**によって、書き込み (メモリからデバイス) 転送の前にプロセッサデータキャッシュがフラッシュされるようになります。 読み取り (デバイスからメモリ) への転送では、すべての**Maptransferex**呼び出しの後にある[**Flushadapterbuffersex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex)ルーチン ([手順 8](#step-8-flush-any-data-that-remains-in-the-cache)を参照) の呼び出し中にキャッシュが無効になります。

## <a name="step-7-receive-notification-when-the-dma-transfer-finishes"></a>手順 7: DMA 転送が終了したときに通知を受け取る


DMA 転送が完了すると、次の2つの方法のいずれかでドライバーに通知されます。

-   バスマスタデバイスのデバイスドライバーへの割り込み
-   システム DMA コントローラーを使用する下位デバイスのドライバー指定の完了ルーチンの実行

システム DMA 転送の場合、ドライバーは入力パラメーターとして**Maptransferex**に完了ルーチンを渡すことができます。
## <a name="step-8-flush-any-data-that-remains-in-the-cache"></a>手順 8: キャッシュに残っているデータをフラッシュする


DMA 転送が完了した後、ドライバーは[**Flushadapterbuffersex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers_ex)ルーチンを呼び出して、キャッシュに残っているすべてのデータをフラッシュする必要があります。 ドライバーは、すべての**Maptransferex**呼び出しの後に、 **Flushadapterbuffersex**を呼び出す必要があります。

**Maptransferex**呼び出しが DMA データバッファーの一部のみをマップする場合、ドライバーは、残りのデータをマップするために**maptransferex**を再度呼び出す必要があります。 複雑な転送では、複数の**Maptransferex**呼び出しが必要になる場合があります。 追加の**Maptransferex**呼び出しごとに、手順 5. ~ 8. を繰り返します。

## <a name="step-9-free-the-dma-channel-and-map-registers"></a>手順 9: DMA チャネルを解放し、レジスタをマップする


DMA データバッファー全体が正常にマップされ、最後の転送が完了すると、ドライバーは[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)ルーチンを呼び出して、dma チャネルと以前に割り当てられたすべてのマップレジスタを解放する必要があります。

## <a name="step-10-release-the-dma-adapter-object"></a>手順 10: DMA アダプターオブジェクトを解放する


すべての DMA 転送が完了し、以前に割り当てられたすべてのマップレジスタが解放されると、ドライバーは[**PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter)ルーチンを呼び出してアダプターオブジェクトを解放します。

 

 




