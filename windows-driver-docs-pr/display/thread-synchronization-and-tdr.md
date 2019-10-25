---
title: スレッドの同期および TDR
description: スレッドの同期および TDR
ms.assetid: 3690ad06-002a-4939-9b04-b87245678464
keywords:
- スレッド化 WDK display、TDR
- 同期 WDK display、TDR
- TDR (タイムアウト検出と復旧) WDK の表示とスレッドの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0898d70c34d915ca2096019e85ab655f649e59c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825501"
---
# <a name="thread-synchronization-and-tdr"></a>スレッドの同期および TDR


次の図は、Windows Display Driver Model (WDDM) のディスプレイミニポートドライバーでスレッドの同期がどのように機能するかを示しています。

![windows vista スレッド同期を示す図](images/lddmsync.png)

ハードウェアのタイムアウトが発生すると、[タイムアウト検出と復旧 (TDR)](timeout-detection-and-recovery.md)プロセスが開始されます。 GPU スケジューラは、ドライバーの[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)関数を呼び出します。これにより、gpu がリセットされます。 *DxgkDdiResetFromTimeout*は、ランタイム電源管理関数[*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)と[*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)を除き、他のすべてのディスプレイミニポートドライバー関数と同期的に呼び出されます。 つまり、 *DxgkDdiResetFromTimeout*スレッドの実行中に、ドライバーで他のスレッドは実行されません。 また、オペレーティングシステムは、 *DxgkDdiResetFromTimeout*の呼び出し中に、どのアプリケーションからもフレームバッファーにアクセスできないことを保証します。そのため、ドライバーはメモリコントローラーのフェーズロックループ (PLL) などをリセットできます。

復旧スレッドによって[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)が実行されている間は、割り込みと遅延プロシージャ呼び出し (dpc) を引き続き呼び出すことができます。 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)関数を使用すると、reset プロシージャの一部をデバイス割り込みと同期することができます。

ドライバーが[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)から戻ると、ほとんどのドライバー関数を再度呼び出すことができ、オペレーティングシステムは不要になったリソースのクリーンアップを開始します。 クリーンアップ期間中は、次のドライバー関数が示されている理由で呼び出されます。

-   ドライバーは、割り当てが削除されたことを通知するために呼び出されます。

    たとえば、割り当てがメモリセグメントにページングされている場合、ドライバーの[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数は、 [**Dxgkarg\_BUILDPAGINGBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)構造体を DXGK\_操作に設定して、**操作**メンバーと共に呼び出されます。\_転送し、**転送サイズ**のメンバーを0に設定して、ドライバーに削除を通知します。 リセット中にコンテンツが失われたため、コンテンツの転送が行われないことに注意してください。

    割り当てがアパーチャセグメントにページングされている場合、ドライバーの[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数は DXGKARG の**操作**メンバー\_BUILDPAGINGBUFFER を DXGK\_operation に設定し、マップを解除\_\_アパーチャ\_セグメントは、割り当てを絞りからマップ解除するようにドライバーに通知します。

-   ドライバーの[*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)関数は、unswizzling アパーチャとセグメントの絞りの範囲を解放するために呼び出されます。

絶対に必要な場合を除き、ドライバーは、上記の呼び出し中に GPU にアクセスしないようにする必要があります。

クリーンアップ期間が終了すると、オペレーティングシステムはドライバーの[*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)関数を呼び出して、クリーンアップが完了したこと、およびレンダリングのためにオペレーティングシステムがアダプターを使用して再開することをドライバーに通知します。

Windows 8 の TDR 機能が更新されている**ことに注意**してください  。 「 [Windows 8 の TDR の変更点」を](tdr-changes-in-windows-8.md)参照してください。

 

 

 





