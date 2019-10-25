---
title: IddCx オブジェクト
description: IddCx では、拡張された UMDF オブジェクトモデルを使用してグラフィックスオブジェクトを表現しています。次のセクションで説明します。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 167b521e1dbf3492b78ea771e3ef9fac274b44e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838891"
---
# <a name="iddcx-objects"></a>IddCx オブジェクト


IddCx では、拡張された UMDF オブジェクトモデルを使用してグラフィックスオブジェクトを表現しています。次のセクションで説明します。 UMDF オブジェクトモデルでは、ドライバー固有のストレージを各 IddCx (つまり、UMDF) オブジェクトに関連付けることができます。詳細については、「UMDF オブジェクトモデル」を参照してください。

## <a name="span-ididdcx_adapterspanspan-ididdcx_adapterspaniddcx_adapter"></a><span id="IDDCX_ADAPTER"></span><span id="iddcx_adapter"></span>IDDCX\_アダプター


このオブジェクトは、2段階のプロセスでドライバーによって作成された1つの論理ディスプレイアダプターを表します。 まず、 [**Iddcxadapterinitasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)コールバック関数を呼び出します。 OS はドライバーの[EvtIddCxAdapterInitFinished](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI を呼び出して、初期化を完了します。

最も単純なケースでは、プラグアンドプレイサブシステムによって作成された UMDF device オブジェクトと、接続されている間接ディスプレイデバイス、およびドライバーが作成する**IDDCX\_アダプター**の間に1対1のマッピングが存在します。 1つの間接ディスプレイドングルに複数のプラグアンドプレイデバイス (2 つの USB デバイス機能など) が含まれているより複雑なシナリオでは、複数の UMDF デバイスに対して1つの**IDDCX\_アダプター**オブジェクトのみを作成するのはドライバーの役割です。作成されたオブジェクト (Pnp デバイスごとに1つ)。 このシナリオでは、ドライバーは次の点を考慮する必要があります。

1. **IDDCX\_アダプター**は、間接表示ソリューションを構成するすべてのデバイスが正常に開始された後に作成する必要があります
2. ドライバーは、アダプターの作成時に1つの**Wdfdevice**を渡す必要があるため、どの UMDF デバイスに渡すかを決定するロジックが必要です。
3. 間接ディスプレイアダプターを構成するいずれかのデバイスでハードウェアエラーが発生した場合、ドライバーは、アダプターを構成するすべてのデバイスをエラーとして報告する必要があります。
間接表示モデルには、明示的な破棄アダプターのコールバックがありません。 アダプター初期化シーケンスが正常に完了すると、初期化時に渡された UMDF デバイスが停止されるまで、アダプターは有効になります。 アダプターを作成するときに、ドライバーは、間接ディスプレイアダプターに関する静的アダプター情報を提供します。

## <a name="span-ididdcx_monitorspanspan-ididdcx_monitorspaniddcx_monitor"></a><span id="IDDCX_MONITOR"></span><span id="iddcx_monitor"></span>IDDCX\_モニター


このオブジェクトは、間接ディスプレイアダプターのいずれかのコネクタに接続されている特定のモニターを表します。

このドライバーは、2段階のプロセスで監視オブジェクトを作成します。 まず、ドライバーは[**Iddcxmonitorcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorcreate)コールバックを呼び出して**IDDCX\_monitor**オブジェクトを作成し、次に[**iddcxmonitorcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)コールバックを呼び出してモニターの到着を完了します。 モニターが取り外されている場合、ドライバーは[**Iddcxmonitordeparture**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitordeparture)コールバックを呼び出してモニターが切断されたことを報告します。これにより、 **IDDCX\_monitor**オブジェクトが破棄されます。 同じモニターが接続解除された後に再接続された場合でも、 **Iddcxmonitordeparture**/**Iddcxmonitordeparture**シーケンスを再度呼び出す必要があります。 **IDDCX\_MONITOR**は**IDDCX\_ADAPTER**オブジェクトの子です。

## <a name="span-ididdcx_swapchainspanspan-ididdcx_swapchainspaniddcx_swapchain"></a><span id="IDDCX_SWAPCHAIN"></span><span id="iddcx_swapchain"></span>IDDCX\_SWAPCHAIN


このオブジェクトは、接続されたモニターに表示するデスクトップイメージを提供するスワップチェーンを表します。 スワップチェーンには、OS が1つのバッファーに次のデスクトップイメージを作成できるようにするための複数のバッファーがあり、間接ディスプレイドライバーが別のバッファーにアクセスしています。 **IDDCX\_スワップチェーン**は**IDDCX\_MONITOR**の子であるため、特定のモニターに対して一度に割り当てられるスワップチェーンは1つだけです。 OS は、 **IDDCX\_SWAPCHAIN**オブジェクトを作成および破棄し、EvtIddCxMonitorAssignSwapChain と EvtIddCxMonitorUnassignSwapChain Ddi 呼び出しを使用してそれらをモニターに割り当て/割り当て解除します。

## <a name="span-ididdcx_opmctxspanspan-ididdcx_opmctxspaniddcx_opmctx"></a><span id="IDDCX_OPMCTX"></span><span id="iddcx_opmctx"></span>IDDCX\_OPMCTX


このオブジェクトは、1つのモニターで出力保護を制御するためにアプリケーションが使用できる1つのアプリケーション OPM コンテキストからのアクティブな OPM コンテキストを表します。 複数の OPM コンテキストは、特定のモニターで同時にアクティブにすることができます。 OS はドライバーを呼び出して、ドライバーの EvtIddCxMonitorOPMCreateProtectedOutput および EvtIddCxMonitorOPMDestroyProtectedOutput DDI 呼び出しを使用して OPM コンテキストを作成および破棄します。

 

 





