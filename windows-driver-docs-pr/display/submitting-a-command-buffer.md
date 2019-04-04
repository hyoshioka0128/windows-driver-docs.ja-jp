---
title: コマンド バッファーを送信します。
description: コマンド バッファーを送信します。
ms.assetid: 3622697a-3989-4756-89d4-c67c81815d49
keywords:
- コマンドの送信、WDK のバッファーを表示
- WDK の表示コマンド バッファーを送信します。
- WDK の表示をコマンド バッファーに渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f37037b3738c32d88eb126b65025dd36d09427c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536669"
---
# <a name="submitting-a-command-buffer"></a>コマンド バッファーを送信します。


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


次の一連の操作を実行して、Windows Vista のグラフィックス スタックをコマンド バッファーを渡す必要があります。

1.  ユーザー モードのディスプレイ ドライバーは、Direct3D ランタイムが、指定された操作を実行する次のユーザー モード ディスプレイ ドライバーの関数の 1 つを呼び出す場合のコマンド バッファーの送信を開始します。

    -   [**存在**](https://msdn.microsoft.com/library/windows/hardware/ff569176)グラフィックスを表示する関数。
    -   [**フラッシュ**](https://msdn.microsoft.com/library/windows/hardware/ff565957)ハードウェア コマンドを送信する関数。
    -   [**ロック**](https://msdn.microsoft.com/library/windows/hardware/ff568213)関数は、現在のコマンド バッチで使用されているリソースをロックします。

    コマンド バッファーがいっぱいのときに、ユーザー モードのディスプレイ ドライバーがそのコマンド バッファーの送信も常に開始されるに注意してください。

2.  Direct3D ランタイムを呼び出して、ユーザー モードのディスプレイ ドライバー [ **pfnRenderCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568923)ランタイムをコマンド バッファーを送信する関数。

3.  DirectX グラフィックスのカーネル サブシステム呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiRender** ](https://msdn.microsoft.com/library/windows/hardware/ff559793)または[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)関数DMA バッファーを記述、ハードウェアの形式でのコマンド バッファーの検証、および使用のサーフェスを記述した割り当て一覧を生成します。 ある DMA バッファーがまだされてパッチは適用されません (つまり、物理アドレスが割り当てられた) に注意してください。
    **注**  場合は、ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出すことによって、コマンド バッファーの送信を開始[**存在**](https://msdn.microsoft.com/library/windows/hardware/ff569176)関数では、グラフィックス サブシステムの呼び出し、ディスプレイ ミニポート ドライバーの[ **DxgkDdiPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff559743)関数、なく[ **DxgkDdiRender** ](https://msdn.microsoft.com/library/windows/hardware/ff559793)または[**DxgkDdiRenderKm**](https://msdn.microsoft.com/library/windows/hardware/ff559800)します。

     

4.  ビデオ メモリ マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587) DMA バッファー、指定された割り当てを移動するページング バッファーと呼ばれる特殊な目的を作成する関数DMA バッファーと GPU からアクセス可能なメモリの間に付属している割り当てリストします。 詳細については、[ビデオ メモリ リソースのページング](paging-video-memory-resources.md)を参照してください。

5.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiPatch** ](https://msdn.microsoft.com/library/windows/hardware/ff559737) DMA バッファー内のリソースへの物理アドレスを割り当てる関数。 ただし、スケジューラを呼び出す必要はありません**DxgkDdiPatch**ページング バッファーの物理アドレスが渡され、中に割り当てられているため、ページング バッファーへの物理アドレスを割り当てる、 [ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)呼び出します。

6.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)ドライバーが GPU 実行単位にページング バッファーをキューに要求します。

7.  GPU スケジューラ呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)ドライバーが GPU 実行単位に DMA バッファーをキューに要求します。 GPU に送信される各 DMA バッファーには、フェンス識別子が含まれています。 GPU では、DMA バッファーの処理が完了すると、GPU は、割り込みを生成します。

8.  ディスプレイのミニポート ドライバーは、割り込みの通知、 [ **DxgkDdiInterruptRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559680)関数。 ディスプレイのミニポート ドライバーから読み取ら GPU、完了した DMA バッファーをフェンスの識別子。

9.  ディスプレイのミニポート ドライバーを呼び出す必要があります、 [ **DxgkCbNotifyInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff559545) DMA バッファーが完了している GPU スケジューラに通知します。

10. ディスプレイのミニポート ドライバーを呼び出す必要があります、 [ **DxgkCbQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff559559)関数遅延プロシージャ呼び出し (DPC) をキューに登録します。

11. DMA バッファー処理のほとんどを処理するために、表示ミニポート ドライバーの DPC に通知されます。

 

 





