---
title: コマンド バッファーの送信
description: コマンド バッファーの送信
ms.assetid: 3622697a-3989-4756-89d4-c67c81815d49
keywords:
- コマンドの送信、WDK のバッファーを表示
- WDK の表示コマンド バッファーを送信します。
- WDK の表示をコマンド バッファーに渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f45a3349afd5c4a1362615f44719c07284266bdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379867"
---
# <a name="submitting-a-command-buffer"></a>コマンド バッファーの送信


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


次の一連の操作を実行して、Windows Vista のグラフィックス スタックをコマンド バッファーを渡す必要があります。

1.  ユーザー モードのディスプレイ ドライバーは、Direct3D ランタイムが、指定された操作を実行する次のユーザー モード ディスプレイ ドライバーの関数の 1 つを呼び出す場合のコマンド バッファーの送信を開始します。

    -   [**存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_present)グラフィックスを表示する関数。
    -   [**フラッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)ハードウェア コマンドを送信する関数。
    -   [**ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)関数は、現在のコマンド バッチで使用されているリソースをロックします。

    コマンド バッファーがいっぱいのときに、ユーザー モードのディスプレイ ドライバーがそのコマンド バッファーの送信も常に開始されるに注意してください。

2.  Direct3D ランタイムを呼び出して、ユーザー モードのディスプレイ ドライバー [ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)ランタイムをコマンド バッファーを送信する関数。

3.  DirectX グラフィックスのカーネル サブシステム呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数DMA バッファーを記述、ハードウェアの形式でのコマンド バッファーの検証、および使用のサーフェスを記述した割り当て一覧を生成します。 ある DMA バッファーがまだされてパッチは適用されません (つまり、物理アドレスが割り当てられた) に注意してください。
    **注**  場合は、ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出すことによって、コマンド バッファーの送信を開始[**存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_present)関数では、グラフィックス サブシステムの呼び出し、ディスプレイ ミニポート ドライバーの[ **DxgkDdiPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_present)関数、なく[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)します。

     

4.  ビデオ メモリ マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) DMA バッファー、指定された割り当てを移動するページング バッファーと呼ばれる特殊な目的を作成する関数DMA バッファーと GPU からアクセス可能なメモリの間に付属している割り当てリストします。 詳細については、次を参照してください。[ビデオ メモリ リソースのページング](paging-video-memory-resources.md)します。

5.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiPatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch) DMA バッファー内のリソースへの物理アドレスを割り当てる関数。 ただし、スケジューラを呼び出す必要はありません**DxgkDdiPatch**ページング バッファーの物理アドレスが渡され、中に割り当てられているため、ページング バッファーへの物理アドレスを割り当てる、 [ *DxgkDdiBuildPagingBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)呼び出します。

6.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)ドライバーが GPU 実行単位にページング バッファーをキューに要求します。

7.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)ドライバーが GPU 実行単位に DMA バッファーをキューに要求します。 GPU に送信される各 DMA バッファーには、フェンス識別子が含まれています。 GPU では、DMA バッファーの処理が完了すると、GPU は、割り込みを生成します。

8.  ディスプレイのミニポート ドライバーは、割り込みの通知、 [ **DxgkDdiInterruptRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)関数。 ディスプレイのミニポート ドライバーから読み取ら GPU、完了した DMA バッファーをフェンスの識別子。

9.  ディスプレイのミニポート ドライバーを呼び出す必要があります、 [ **DxgkCbNotifyInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt) DMA バッファーが完了している GPU スケジューラに通知します。

10. ディスプレイのミニポート ドライバーを呼び出す必要があります、 [ **DxgkCbQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)関数遅延プロシージャ呼び出し (DPC) をキューに登録します。

11. DMA バッファー処理のほとんどを処理するために、表示ミニポート ドライバーの DPC に通知されます。

 

 





