---
title: オーディオ ミニポート オブジェクトのインターフェイス
description: オーディオ ミニポート オブジェクトのインターフェイス
ms.assetid: 2e79ad90-fecc-47a7-b487-809325a16239
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b5baf036d1df4b4ea6ee5485223241def70c132
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358313"
---
# <a name="audio-miniport-object-interfaces"></a>オーディオ ミニポート オブジェクトのインターフェイス


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ミニポート オブジェクトのインターフェイスについて説明します。 これには次のものがあります。

-   **IMiniport**、他のすべてのオーディオ ミニポート オブジェクト インターフェイスの派生元の基本型であります。

-   オーディオ ミニポート オブジェクト Dmu、MIDI、トポロジ、WaveCyclic、WavePci および WaveRT ミニポート ドライバー インターフェイスを提供します (を参照してください[デバイスをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)) から派生する**IMiniport**

オーディオ ミニポート オブジェクトのインターフェイスは、ミニポート ドライバーがポート ドライバーに提示する主なインターフェイスです。 アダプターのドライバーでは、そのデバイスのポートおよびミニポートのドライバーをまとめてバインドすることによって、オーディオ デバイスの KS フィルターを形成します。 オーディオ ポート オブジェクトの呼び出し、割り当てを行う[ **iport::init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)メソッドとオーディオ ミニポート オブジェクトへの参照を呼び出しのパラメーターとして渡します。 コード例で[サブデバイス作成](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)このプロセスを示しています。

このセクションでは、次のオーディオ ミニポート オブジェクト インターフェイスについて説明します。

[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)

 

 





