---
title: DMA バッファーの分割
description: DMA バッファーの分割
ms.assetid: 6b35d5e2-f8aa-478a-a5a0-9f519ff0ba6f
keywords:
- DMA バッファーの分割、WDK の表示
- DMA バッファーの分割
- 分割ポイント WDK の表示
- 更新プログラムの場所には、WDK の表示が一覧表示されます。
- WDK の表示の DMA バッファーを優先
- DMA バッファー WDK の表示、プリエンプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebb3221bf470bf50fc66bc35d0e7339490f25d20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376043"
---
# <a name="splitting-a-dma-buffer"></a>DMA バッファーの分割


## <span id="ddk_splitting_a_dma_buffer_gg"></span><span id="DDK_SPLITTING_A_DMA_BUFFER_GG"></span>


分割ポイントを実行するには、少ない GPU リソースを必要とする小さな作業項目にディスプレイのミニポート ドライバーによって送信される大規模な作業項目を分割するビデオ メモリ マネージャーによって使用されます。 たとえば、大きな DMA バッファーでは、ローカル ビデオ メモリまたは非ローカル メモリに収まらない可能性がある割り当てのセットを参照可能性があります。 このような作業項目を処理する唯一の方法では、GPU リソースが必要とする複数の小さい作業項目に分割します。

**注**   DMA バッファーの分割と DMA バッファー プリエンプションは、別の独立した概念です。 ディスプレイのミニポート ドライバーでは、DMA バッファー プリエンプションが可能な GPU を搭載したシステム上であっても分割 DMA バッファーを常にサポートする必要があります。 コンテキストの保存場所と復元は、gpu を搭載したシステムでは可能であれば、さまざまな GPU コンテキストから別の DMA バッファーを GPU スケジューラ スケジュール分割部分 DMA バッファー背面へ戻るは分割部分のことを確認するがインターリーブされていないできません。 ただし、ページング操作は DMA バッファーの分割部分の間で必要なために、分割 DMA バッファーの部分間ページング バッファーを送信する必要があります。
ドライバーを使用して、アプリケーションの DMA ストリームを構築する各分割ポイントは、ビデオ メモリ マネージャーによって使用されます。 送信された DMA バッファーは、その位置に挿入される可能性がある潜在的なページング バッファーのアカウントに分岐点それぞれ後、十分な GPU の状態を再設定する必要があります。

 

ディスプレイのミニポート ドライバーを分割ポイントを指定するには、内の値を指定します、 **SplitOffset**と**SlotId**のメンバー、 [ **D3DDDI\_PATCHLOCATIONLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist)で参照されている各割り当ての構造、 **AllocationIndex** D3DDDI のメンバー\_PATCHLOCATIONLIST します。 配列を使用して、必要なディメンションを作成しているビデオ メモリ マネージャー特定 DMA バッファー内の割り当ての使用率を追跡するために、 **MaxAllocationListSlotId**のメンバー、 [ **DXGK\_DRIVERCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)を呼び出すことによって、ドライバーが提供する構造体の[ **DxgkDdiQueryAdapterInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)関数。 この配列は、ゼロで初期化され、更新プログラムの場所の一覧の分割部分のエントリの処理に入力されます。 **SlotId**のメンバー **D3DDDI\_PATCHLOCATIONLIST**場所が、リソース テーブルの行を更新する必要がありますを示す、修正プログラムの中に、 **SplitOffset**メンバーは、割り当てが必要になる DMA バッファー内のオフセットを示します。 DMA バッファーで指定された時点まで実行できる**SplitOffset**利用可能にする GPU リソースなし。 同様に、新しい更新プログラムの場所エントリの部分を分割する場合を指す同じ**SlotId**、前の割り当ては、新しい割り当て、置き換えられるはおよび以前の割り当ては不要です (つまり、前の割り当てできますページアウト)。

DMA バッファーに必要なリソースでのページングと、ビデオ メモリ マネージャーは、最初の要素で始まる、最後の要素に向かって下へ移動して、修正プログラムの場所の一覧を処理します。 [ **D3DDDI\_PATCHLOCATIONLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist)ドライバーがいっぱいになる要素の値を含める必要があります、 **SplitOffset**メンバーは要素が確実に増加する (つまり、割り当てからストリームで使用する順序で表示する必要があります)。 割り当てが用意されている順序で更新プログラムの場所の一覧で参照されているビデオ メモリ マネージャー ページ。 場所、ビデオ メモリ マネージャーできますページ-ではありません、割り当てがメモリ不足条件によるポイントに達すると、ビデオ メモリ マネージャーは、GPU のスケジューラの実行する準備をして DMA バッファーの現在の一部を送信します。 DMA バッファーが最大実行前の分岐点の先頭から、 **SplitOffset**でにできませんでしたが、割り当ての指定された値。 送信されると、ビデオ メモリ マネージャーは、現在のオフセット、DMA ストリームで、リソース テーブルを使用して分割に必要な割り当ての一覧を決定します。 テーブルのすべての割り当てが、現在の物理的な場所に保持されるは、一方、使用されなくなった他の割り当てが削除される可能性があります。 ビデオ メモリ マネージャーは、可能性のある複数回を分割することはもう一度、更新プログラムの場所の一覧を処理に続きます。

ドライバーは、割り当てがバインドまたはバインド解除するたびに分割ポイントを指定する必要があります。 割り当てがバインドではないことを指定するドライバーを指定できます、 **NULL**でハンドルを割り当て、 **hDeviceSpecificAllocation**のメンバー、 [ **DXGK\_ALLOCATIONLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationlist)で適切な値を持つ、 **SlotId** 、関連付けられているメンバー [ **D3DDDI\_PATCHLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_patchlocationlist). ビデオ メモリ マネージャーがメモリの複雑な配置の問題を解決できる可能性を向上させる大規模なリソースは、ドライバーのバインドを解除する必要があります。

同様に、ドライバーは、すべての分割ポイントでの大規模なリソースを再設定する必要があります。 分割ポイントを作成する際は、ビデオ メモリ マネージャーを強制的に以前の割り当てを以前にバインドされた割り当てのままにします。 これにより、以前にバインドされた割り当て制限のない場合、解決されているメモリの複雑な配置の問題を解決するために失敗につながる可能性のあるメモリの断片化。 分割時点の状態を計算するときにビデオ メモリ マネージャーがどのスロット識別子を決定します (**SlotId**) は、その再プログラムされている分岐点 (各更新プログラムの場所のリスト要素を同じを共有する**SplitOffset**と他の要素の値)、この分割ポイントに、配置制限が無視されます。 など、ドライバーは、64 MB のテクスチャを使用している場合すべて分割ポイントでは、そのテクスチャを再プログラミングの柔軟性がビデオ メモリ マネージャー、必要に応じて分割ポイントとの間、メモリ内でそのテクスチャを移動します。

 

 





