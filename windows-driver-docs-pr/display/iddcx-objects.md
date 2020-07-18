---
title: IddCx オブジェクト
description: IddCx では、拡張された UMDF オブジェクトモデルを使用してグラフィックスオブジェクトを表現しています。次のセクションで説明します。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 07/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5ab7ebb0160be42da0a1020913a240c75cd7fbca
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459216"
---
# <a name="iddcx-objects"></a>IddCx オブジェクト

[IddCx](/windows-hardware/drivers/ddi/iddcx/) (間接ディスプレイドライバークラス拡張) は、拡張された UMDF オブジェクトモデルを使用して、間接ディスプレイデバイスのコンポーネントを表します。 [Umdf](/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)オブジェクトモデルでは、ドライバー固有の記憶域を各 IddCx (つまり、UMDF) オブジェクトに関連付けることができます。 詳細については、「 [UMDF オブジェクトモデル](/windows-hardware/drivers/wdf/umdf-objects-and-interfaces)」を参照してください。

IDD オブジェクトの作成順序は次のとおりです。

* ドライバーは、最初に**IDDCX_ADAPTER**オブジェクトを作成します。
* 次に、ドライバーは**IDDCX_MONITOR**オブジェクトを作成します。
* **IDDCX_ADAPTER**オブジェクトと**IDDCX_MONITOR**オブジェクトを作成すると、OS によって**IDDCX_SWAPCHAIN**オブジェクトと**IDDCX_OPMCTX**オブジェクトが作成され、ドライバーに送信されます。

以下のセクションでは、これらのオブジェクトの詳細について説明します。

## <a name="iddcx_adapter"></a>IDDCX_ADAPTER

このオブジェクトは、次の2段階のプロセスでドライバーによって作成された1つの論理ディスプレイアダプターを表します。

* ドライバーは[**Iddcxadapterinitasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)コールバック関数を呼び出します。
* OS は、ドライバーの[*EvtIddCxAdapterInitFinished*](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI を呼び出して、初期化を完了します。

IDD モデルに明示的な破棄アダプターのコールバックがありません。 アダプター初期化シーケンスが正常に完了すると、初期化時に渡された UMDF デバイスが停止されるまで、アダプターは有効になります。 アダプターを作成するときに、ドライバーは、間接ディスプレイアダプターに関する静的アダプター情報を提供します。

### <a name="handling-multifunction-devices"></a>多機能デバイスの処理

最も単純なケースでは、アタッチされた間接ディスプレイデバイスのプラグアンドプレイサブシステムによって作成される UMDF device オブジェクトと、間接ディスプレイドライバー (IDD) によって作成される**IDDCX_ADAPTER**オブジェクトの間に、一対一のマッピングが存在します。

1つの間接ディスプレイドングルに複数のプラグアンドプレイデバイスが含まれている場合は、より複雑なシナリオが発生する可能性があります。 たとえば、間接表示ソリューションには、マイク (オーディオドライバー) やカメラ (ビデオドライバー) などの複数の PnP デバイス機能がある場合があります。 このような場合は、各 PnP デバイス用に作成された複数の UMDF デバイスオブジェクトに対して、1つの**IDDCX_ADAPTER**オブジェクトを作成する必要があります。 このシナリオでは、ドライバーは次の点を考慮する必要があります。

* **IDDCX_ADAPTER**は、間接表示ソリューションを構成するすべての PnP デバイスが正常に開始された後に作成する必要があります。
* ドライバーは、アダプターの作成時に1つの**Wdfdevice**を渡す必要があるため、渡す UMDF デバイスを決定するロジックが必要です。
* 間接ディスプレイアダプターを構成するいずれかのデバイスでハードウェアエラーが発生した場合、ドライバーは、アダプターを構成するすべてのデバイスをエラーとして報告する必要があります。

## <a name="iddcx_monitor"></a>IDDCX_MONITOR

このオブジェクトは、間接ディスプレイアダプターのいずれかのコネクタに接続されている特定のモニターを表します。

このドライバーは、次の2段階のプロセスで監視オブジェクトを作成します。

* まず、 [**Iddcxmonitorcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorcreate)コールバックを呼び出して、 **IDDCX_MONITOR**オブジェクトを作成します。
* 次に、 [**Iddcxmonitorarrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)コールバックを呼び出して、モニターの到着を完了します。

モニターが取り外されると、ドライバーは[**Iddcxmonitordeparture**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitordeparture)コールバックを呼び出してモニターが切断されたことを報告します。これにより、 **IDDCX_MONITOR**オブジェクトが破棄されます。 同じモニターが接続解除された後に再接続された場合でも、 **iddcxmonitordeparture**の / **iddcxmonitordeparture**シーケンスを再度呼び出す必要があります。

**IDDCX_MONITOR**は**IDDCX_ADAPTER**オブジェクトの子です。

## <a name="iddcx_swapchain"></a>IDDCX_SWAPCHAIN

このオブジェクトは、接続されたモニターに表示するデスクトップイメージを提供する[スワップチェーン](https://docs.microsoft.com/windows/win32/direct3d12/swap-chains)を表します。 スワップチェーンには複数のバッファーがあるため、OS は次のデスクトップイメージを1つのバッファーに作成できますが、IDD は別のバッファーにアクセスします。 **IDDCX_SWAPCHAIN**は**IDDCX_MONITOR**の子なので、指定されたモニターには常に1つのスワップチェーンのみが割り当てられます。

OS は、 **IDDCX_SWAPCHAIN**オブジェクトを作成して破棄し、 [**EvtIddCxMonitorAssignSwapChain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain)と[**EvtIddCxMonitorUnassignSwapChain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_unassign_swapchain) Ddi 呼び出しを使用してそれらのオブジェクトをモニターに割り当て/割り当て解除します。

## <a name="iddcx_opmctx"></a>IDDCX_OPMCTX

このオブジェクトは、単一のアプリケーション OPM コンテキストから、1つのモニターで出力保護を制御するために使用できる、active [Output Protection Manager](https://docs.microsoft.com/windows/win32/medfound/output-protection-manager) (OPM) コンテキストを表します。 複数の OPM コンテキストは、特定のモニターで同時にアクティブにすることができます。 OS はドライバーを呼び出して、ドライバーの[**EvtIddCxMonitorOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_opm_create_protected_output)および[**EvtIddCxMonitorOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_opm_destroy_protected_output) DDI 呼び出しを使用して OPM コンテキストを作成および破棄します。
