---
title: オーディオ リソースの再調整と予期しない削除操作中におけるメモリ バッファーの管理
description: PnP の再調整は、メモリリソースを再割り当てする必要がある特定の PCI シナリオで使用されます。 問題を回避するには、メモリバッファーを適切に管理する必要があります。
ms.date: 04/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6f20a301ebb183ad92a66641bf7b6f88ed51dad2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832657"
---
# <a name="managing-memory-buffers-during-audio-resource-rebalance-and-surprise-removal-operations"></a>オーディオ リソースの再調整と予期しない削除操作中におけるメモリ バッファーの管理

## <a name="pnp-rebalance-overview"></a>PnP の再調整の概要

PnP の再調整は、メモリリソースを再割り当てする必要がある特定の PCI シナリオで使用されます。 PnP の再調整は、Windows 10 バージョン1511以降のバージョンの Windows で使用できます。 再調整に関する一般的な情報については、「 [PortCls Audio Drivers の PnP](implement-pnp-rebalance-for-portcls-audio-drivers.md)再調整を実装する」を参照してください。

## <a name="pnp-surprise-removal-overview"></a>PnP の突然の削除の概要

PnP "突然削除" (SR) は、デバイスがコンピューターから予期せず取り外され、i/o 操作で使用できなくなった場合に発生します。 詳細については、「 [PnP デバイスの状態遷移](https://docs.microsoft.com/windows-hardware/drivers/kernel/state-transitions-for-pnp-devices)と[IRP_MN_SURPRISE_REMOVAL 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)」を参照してください。

## <a name="managing-memory-buffers-during-audio-resource-rebalance-and-surprise-removal-operations"></a>オーディオ リソースの再調整と予期しない削除操作中におけるメモリ バッファーの管理

このセクションでは、メモリバッファーを管理する方法と、オーディオリソースの再調整時にメモリバッファーをクリーンアップするための一連の操作と HD オーディオコーデックドライバーの PnP SR 操作について説明します。

このトピックで説明されているバッファー管理アプローチのオペレーティングシステムのサポートは、2019年5月の更新後の Windows の次の主な機能リリースで利用できることに注意してください。

サポートするメモリバッファーの割り当てと解放が適切に実行されない場合は、メモリの破損、ソフトハング、および[バグチェック 0x9f: DRIVER_POWER_STATE_FAILURE](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)などの障害が発生する可能性があります。


**ストリームハンドルの動作を閉じる**

Portcls が close ストリームハンドルを受け取ると、portcls は次の関数を呼び出してストリームの状態を停止に設定し、バッファーを解放します。

*ストリームの状態を設定*します (ストリームがまだ停止状態になっていない場合)。

[IMiniportWaveRTStream:: SetState](https://msdn.microsoft.com/en-us/library/windows/hardware/ff536756(v=vs.85).aspx)

*リリースバッファー*  

[IMiniportWaveRTStream:: FreeAudioBuffer](https://msdn.microsoft.com/library/windows/hardware/ff536745)または[IMiniportWaveRTStreamNotification:: FreeBufferWithNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)

Portcls ミニポートドライバーが、SR/STOP 操作中にドライバーによって既に停止されている場合 (つまり、前に SR/STOP が到着した場合) に、状態が大きい値から小さい値に正常に移行することに注意してください。ハンドルを閉じる要求)。

**バッファー処理**


通常の操作中にストリームが閉じられると、portcls は Wave RT のコールバックを呼び出して、ドライバーが DMA 操作を停止し、関連付けられているバッファーを解放できるようにします。

[IMiniportWaveRTStream:: SetState](https://msdn.microsoft.com/en-us/library/windows/hardware/ff536756(v=vs.85).aspx) -> SETDMAENGINESTATE (HD AUDIO Bus DDI)。 DMA を開始または一時停止するためのアクションを実行します。

[IMiniportWaveRTStream:: FreeAudioBuffer](https://msdn.microsoft.com/library/windows/hardware/ff536745)または[IMiniportWaveRTStreamNotification:: FreeBufferWithNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)-> FreeDmaBuffer (HD audio Bus DDI)。

IMiniportWaveRTStream [Notification] のデストラクター-> FreeDmaEngine (HD Audio Bus DDI)。 

デバイスが突然削除されると、ミニポートは、開いているストリームハンドルが閉じるのを待たずにすべての h/w リソースを解放する必要があります。 これは、 [Pcdisptachirp](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp) DDI で PnP 要求を PortCls に転送する前に、すべての割り当て済み DMA エンジンを停止、リセット、および解放する必要があることを意味します。 一方、ミニポートは、ストリームハンドルが閉じるまでオーディオ Wave RT のバッファーを解放しないようにする必要があります。また、PortCls は、FreeAudioBuffer/FreeBufferWithNotification コールバックを使用してミニポートに通知します。

再調整をサポートするように選択されたためにデバイスが停止した場合、ミニポートは、開いているストリームハンドルが閉じるのを待たずに、すべてのハードウェアリソースを解放する必要があります。 これは、portcls によって呼び出される PnP コールバックで、ミニポートがすべての割り当て済み DMA エンジンを停止、リセット、および解放する必要があることを意味します。 一方、ミニポートは、ストリームハンドルが閉じるまでオーディオ Wave RT のバッファーを解放しないようにする必要があります。また、PortCls は、FreeAudioBuffer/FreeBufferWithNotification コールバックを使用してミニポートに通知します。

通常の close ストリーム操作は、SR/Stop 操作と同時に発生する可能性があることに注意してください。これは、ミニポートがこれらのスレッド間の適切な同期を実装する必要があることを意味します。

SR/STOP スレッドと Close スレッドの間に適切なシリアル化コードが存在することを前提とした操作の例を次に示します。


終了時:

```
STOP_DMA

FREE_BUFFER

FREE_DMA_ENGINE
```

SR/Stop の場合:

```
STOP_DMA

FREE_DMA_ENGINE
```

これは、擬似コードでのこれらの操作の定義です。

```
STOP_DMA:
if (DmaEngineState != ResetState)
{
\\Set DMA Engine state to not running
SetDmaEngineState(context, StopState, 1, &dma);
SetDmaEngineState(context, ResetState, 1, &dma);
DmaEngineState = ResetState;
}
```


```
FREE_BUFFER:
\\Free DMA buffer
FreeDmaEBuffer(context, dma);
```


```
FREE_DMA_ENGINE:
if (DMAEngineAllocated==true)
{
\\Free DMA engine
FreeDmaEngine (context, dma);
DMAEngineAllocated=false
}
```

詳しくは、次のトピックをご覧ください。

[PSET_DMA_ENGINE_STATE callback 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[HDAUDIO_STREAM_STATE 列挙型](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/hdaudio/ne-hdaudio-_hdaudio_stream_state)

[PFREE_DMA_ENGINE callback 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[PSET_DMA_ENGINE_STATE callback 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[IMiniportWaveRTStreamNotification インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification) 

[IMiniportWaveRTStreamNotification:: FreeBufferWithNotification メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstreamnotification-freebufferwithnotification)

[PcDisptachIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp)