---
title: オーディオ ミニポート オブジェクトのインターフェイス
description: オーディオ ミニポート オブジェクトのインターフェイス
ms.assetid: 2e79ad90-fecc-47a7-b487-809325a16239
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 704d8bf992c7357dd2e948251265fac1090a79a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833675"
---
# <a name="audio-miniport-object-interfaces"></a>オーディオ ミニポート オブジェクトのインターフェイス


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオミニポートオブジェクトインターフェイスについて説明します。 これには次のものがあります。

-   **IMiniport**。これは、他のすべてのオーディオミニポートオブジェクトインターフェイスの派生元の基本型です。

-   オーディオミニポートオブジェクトは、DMus、MIDI、トポロジ、WaveCyclic、WavePci、および WaveRT のミニポートドライバーのインターフェイスを提供します (「[デバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)」を参照してください)。これは**IMiniport**から派生したものです。

オーディオミニポートオブジェクトインターフェイスは、ミニポートドライバーがポートドライバーに提示する主要なインターフェイスです。 アダプタードライバーは、そのデバイスのポートとミニポートドライバーを結合することによって、オーディオデバイスの KS フィルターを形成します。 バインディングは、オーディオポートオブジェクトの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出し、オーディオミニポートオブジェクトへの参照を呼び出しパラメーターとして渡すことによって実現されます。 [サブデバイス作成](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)のコード例では、このプロセスを示しています。

このセクションでは、次のオーディオミニポートオブジェクトインターフェイスについて説明します。

[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)

 

 





