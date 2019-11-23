---
title: コマンド バッファーの送信
description: コマンド バッファーの送信
ms.assetid: 3622697a-3989-4756-89d4-c67c81815d49
keywords:
- コマンドバッファー WDK 表示、送信
- コマンドバッファーの送信 WDK 表示
- コマンドバッファーを渡す WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473ec72edca76056ae70e81df6c665021669acac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829428"
---
# <a name="submitting-a-command-buffer"></a>コマンド バッファーの送信


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


Windows Vista のグラフィックススタックを使用してコマンドバッファーを渡すには、次の一連の操作を実行する必要があります。

1.  ユーザーモードの表示ドライバーは、指定された操作を実行するために、Direct3D ランタイムが次のユーザーモード表示ドライバー関数のいずれかを呼び出すと、コマンドバッファーの送信を開始します。

    -   グラフィックスを表示する[**現在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)の関数。
    -   ハードウェアコマンドを送信するための[**フラッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)関数。
    -   現在のコマンドバッチで使用されているリソースをロックするための[**ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)関数。

    ユーザーモードの表示ドライバーは、コマンドバッファーがいっぱいになったときに常にコマンドバッファーの送信を開始することにも注意してください。

2.  ユーザーモード表示ドライバーは、Direct3D ランタイムの[**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)関数を呼び出して、コマンドバッファーをランタイムに送信します。

3.  DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの[**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数を呼び出して、コマンドバッファーを検証し、ハードウェアの形式で DMA バッファーを書き込み、使用されているサーフェスを説明する割り当てリストを生成します。 DMA バッファーにはまだパッチが適用されていないことに注意してください (つまり、割り当てられた物理アドレス)。
    **注**   ユーザーモード表示ドライバーの[**Present**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)関数を呼び出すことによってランタイムがコマンドバッファーの送信を開始した場合、グラフィックスサブシステムは、 [**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)ではなく、ディスプレイミニポートドライバーの[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)関数を呼び出します。

     

4.  ビデオメモリマネージャーは、ディスプレイミニポートドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出して、ページングバッファーと呼ばれる特殊な目的の dma バッファーを作成します。これにより、dma バッファーに付属する割り当てリストで指定された割り当てが、GPU からアクセス可能なメモリに移動します。 詳細については、「[ビデオメモリリソースのページング](paging-video-memory-resources.md)」を参照してください。

5.  GPU スケジューラは、ディスプレイミニポートドライバーの[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)関数を呼び出して、DMA バッファー内のリソースに物理アドレスを割り当てます。 ただし、ページングバッファーの物理アドレスが渡され、 [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)呼び出し中に割り当てられたため、スケジューラは**DxgkDdiPatch**を呼び出して物理アドレスをページングバッファーに割り当てる必要はありません。

6.  GPU スケジューラは、ディスプレイミニポートドライバーの[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数を呼び出して、ドライバーが GPU 実行単位へのページングバッファーをキューに格納するように要求します。

7.  GPU スケジューラは、ディスプレイミニポートドライバーの[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数を呼び出して、ドライバーが GPU 実行単位に対して DMA バッファーをキューに格納するように要求します。 GPU に送信される各 DMA バッファーには、フェンス識別子が含まれます。 GPU が DMA バッファーの処理を終了すると、GPU によって割り込みが生成されます。

8.  ディスプレイミニポートドライバーには、 [**DxgkDdiInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)関数の割り込みが通知されます。 表示ミニポートドライバーは、完了したばかりの DMA バッファーのフェンス識別子を GPU から読み取る必要があります。

9.  ディスプレイミニポートドライバーは、 [**Dxgkcbnotifyinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)関数を呼び出して、DMA バッファーが完了したことを GPU スケジューラに通知する必要があります。

10. ディスプレイミニポートドライバーは、遅延プロシージャ呼び出し (DPC) をキューにするために[**DxgkCbQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)関数を呼び出す必要があります。

11. ディスプレイミニポートドライバーの DPC には、DMA バッファー処理のほとんどを処理するように通知されます。

 

 





