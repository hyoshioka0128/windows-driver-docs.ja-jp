---
title: IddCx オブジェクト
description: IddCx グラフィック オブジェクトを表す拡張 UMDF オブジェクト モデルを使用して、それらは次のセクションで説明します。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67831ae640752456b51bf06d7a248632039dd571
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380196"
---
# <a name="iddcx-objects"></a>IddCx オブジェクト


IddCx グラフィック オブジェクトを表す拡張 UMDF オブジェクト モデルを使用して、それらは次のセクションで説明します。 UMDF オブジェクト モデルにより、各 IddCx に関連するドライバーの特定のストレージ (つまり UMDF) オブジェクト、詳細については、UMDF オブジェクト モデルを参照してください

## <a name="span-ididdcxadapterspanspan-ididdcxadapterspaniddcxadapter"></a><span id="IDDCX_ADAPTER"></span><span id="iddcx_adapter"></span>IDDCX\_ADAPTER


このオブジェクトは、2 段階のプロセスで、ドライバーによって作成された 1 つの論理ディスプレイ アダプターを表します。 最初に、呼び出し、 [ **IddCxAdapterInitAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxadapterinitasync)コールバック関数と OS の呼び出し、ドライバーの[EvtIddCxAdapterInitFinished](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI 初期化を完了します。

最も簡単なケースでは、接続されている間接のディスプレイ デバイスのプラグ アンド プレイ サブシステムによって作成された UMDF デバイス オブジェクトの間で一対一のマッピングと**IDDCX\_アダプター**ドライバーを作成します。 1 つだけを作成するドライバーの責任はより複雑なシナリオの 1 つの間接的な表示ドングルに複数のプラグ アンド プレイ デバイス (例: 2 USB デバイスの機能) が含まれていますで**IDDCX\_アダプター**オブジェクト複数の umdf デバイス オブジェクトを作成、Pnp デバイスごとに 1 つ。 ドライバーは、このシナリオでは、次を考慮する必要があります。

1. **IDDCX\_アダプター**間接表示ソリューションを構成するすべてのデバイスが正常に開始された後にのみ作成する必要があります
2. ドライバーは、1 つを渡すには**WDFDEVICE**のために合格する UMDF デバイスを決定するためのロジックに要する、アダプターを作成する場合。
3. ハードウェア エラーがあるすべての間接的なディスプレイ アダプターを構成するデバイスは、ドライバーはエラーになっているとアダプターを構成するすべてのデバイスを報告する必要があります。
間接的な表示モデルは、明示的なアダプターのコールバックの破棄はありません。 アダプターの初期化シーケンスが正常に完了したら、アダプターの値は初期化時に渡された UMDF デバイスを停止するまで有効です。 アダプターを作成するときに、ドライバーは、間接的なディスプレイ アダプターに関する静的アダプターの情報を提供します。

## <a name="span-ididdcxmonitorspanspan-ididdcxmonitorspaniddcxmonitor"></a><span id="IDDCX_MONITOR"></span><span id="iddcx_monitor"></span>IDDCX\_モニター


このオブジェクトは、間接的なディスプレイ アダプターのコネクタのいずれかに接続されている特定のモニターを表します。

ドライバーは、2 段階のプロセスで監視オブジェクトを作成します。 まず、ドライバーを呼び出し、 [ **IddCxMonitorCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitorcreate)コールバックを作成する、 **IDDCX\_モニター**呼び出し、オブジェクト[ **IddCxMonitorArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitorarrival)モニターの到着を完了するコールバック。 モニターが接続されている場合、ドライバーの呼び出し、 [ **IddCxMonitorDeparture** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitordeparture)モニターをレポートするコールバックが、接続されていないは、 **IDDCX\_モニター**オブジェクトを破棄します。 同じのモニターが再接続し、ugged 解除しない場合でも、 **IddCxMonitorDeparture**/**IddCxMonitorArrival**シーケンスをもう一度呼び出す必要があります。 **IDDCX\_モニター**の子であり、 **IDDCX\_アダプター**オブジェクト。

## <a name="span-ididdcxswapchainspanspan-ididdcxswapchainspaniddcxswapchain"></a><span id="IDDCX_SWAPCHAIN"></span><span id="iddcx_swapchain"></span>IDDCX\_SWAPCHAIN


このオブジェクトは、接続されているモニターに表示するデスクトップ イメージを提供するスワップを表します。 スワップは、間接的なディスプレイ ドライバーは別のバッファーにアクセスするときに、1 つのバッファーの次のデスクトップ イメージを作成する OS を許可する複数のバッファー。 **IDDCX\_スワップ**の子である、 **IDDCX\_モニター**はだけ特定のモニターに割り当てられている 1 つのスワップ、いつでもようにします。 OS を作成し、破棄、 **IDDCX\_スワップ**オブジェクトし、割り当て/割り当てが解除して EvtIddCxMonitorAssignSwapChain と EvtIddCxMonitorUnassignSwapChain Ddi 呼び出しを使用して監視します。

## <a name="span-ididdcxopmctxspanspan-ididdcxopmctxspaniddcxopmctx"></a><span id="IDDCX_OPMCTX"></span><span id="iddcx_opmctx"></span>IDDCX\_OPMCTX


このオブジェクトは、1 つのアプリケーション、アプリケーションは、1 つのモニターでの出力保護の制御に使用できる OPM コンテキストからのアクティブな OPM コンテキストを表します。 同時に指定した monitor でアクティブにできる複数の OPM コンテキストです。 OS の呼び出し、ドライバーを作成して、ドライバーの EvtIddCxMonitorOPMCreateProtectedOutput を使用して OPM コンテキストを破棄し、EvtIddCxMonitorOPMDestroyProtectedOutput DDI を呼び出します。

 

 





