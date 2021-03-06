---
title: スレッドの同期および TDR
description: スレッドの同期および TDR
ms.assetid: 3690ad06-002a-4939-9b04-b87245678464
keywords:
- WDK の表示、TDR スレッド処理
- WDK の表示、TDR の同期
- (タイムアウト検出と回復) TDR WDK の表示、およびスレッドの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9d69ebfec70ff8e2a990446a10ce0fc8ebfae75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354699"
---
# <a name="thread-synchronization-and-tdr"></a>スレッドの同期および TDR


次の図は、ディスプレイのミニポート ドライバー Windows 表示 Driver Model (WDDM) でのスレッドの同期のしくみを示しています。

![windows vista のスレッドの同期を示す図](images/lddmsync.png)

ハードウェアのタイムアウトが発生した場合、[タイムアウト検出と復旧 (TDR)](timeout-detection-and-recovery.md)処理を開始します。 GPU スケジューラ呼び出してドライバーの[ *DxgkDdiResetFromTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数で、GPU をリセットします。 *DxgkDdiResetFromTimeout*がその他の表示ミニポート ドライバー機能、実行時の電源管理関数を除くで同期的に呼び出された[ *DxgkDdiSetPowerComponentFState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)と[ *DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)します。 つまり、他のスレッドなしで実行中にドライバー、 *DxgkDdiResetFromTimeout*スレッドの実行。 オペレーティング システムが呼び出し中に任意のアプリケーションからフレーム バッファーへのアクセスは発生しないことを保証しても*DxgkDdiResetFromTimeout*。 したがって、ドライバーでは、メモリ コント ローラー フェーズ ロックされているループ (PLL) をこれにリセットします。

復旧スレッドを実行しながら[ *DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)、割り込みを遅延プロシージャ呼び出し (Dpc) が呼び出され続けますことができます。 [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)デバイス割り込みとリセットの手順の一部を同期する関数を使用できます。

ドライバーから返された後[ *DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)、もう一度、ほとんどのドライバー関数を呼び出すことができます、およびオペレーティング システムの起動時に不要になったリソースをクリーンアップします。 クリーンアップの期間中に指定された上の理由から、次のドライバー関数が呼び出されます。

-   ドライバーが削除される割り当てについての通知と呼ばれます。

    たとえば、割り当て、メモリ内でページを送信した場合をセグメント化、ドライバーの[ *DxgkDdiBuildPagingBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出すと、**操作**のメンバー[**DXGKARG\_BUILDPAGINGBUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer) DXGK に設定\_操作\_転送を使用して、 **Transfer.Size**メンバー削除、ドライバーに通知する 0 に設定します。 コンテンツの転送がないこと関連するコンテンツが、リセット時に失われたために注意してください。

    ページ割り当てを aperture で送信した場合は、セグメント化、ドライバーの[ *DxgkDdiBuildPagingBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出すと、**操作**DXGKARGのメンバー\_BUILDPAGINGBUFFER 設定 DXGK\_操作\_UNMAP\_APERTURE\_開口部からの割り当てを解除するドライバーに通知するセグメント。

-   ドライバーの[ *DxgkDdiReleaseSwizzlingRange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)アンスィズル aperture とセグメントの開口部の範囲を解放する関数が呼び出されます。

ドライバーにアクセスしないように、上記の中に GPU を呼び出す場合を除き、どうしても必要な。

オペレーティング システムは、ドライバーの呼び出しますクリーンアップ期間が終了したら[ *DxgkDdiRestartFromTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)そのクリーンアップが完了すると、ドライバーに通知する関数と、オペレーティング システムが再開されますアダプターを使用して、レンダリングします。

**注**  Windows 8 の TDR の機能が更新されました。 参照してください[Windows 8 での TDR 変更](tdr-changes-in-windows-8.md)します。

 

 

 





