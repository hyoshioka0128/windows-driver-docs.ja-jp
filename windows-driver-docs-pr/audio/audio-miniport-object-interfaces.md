---
title: オーディオ ミニポート オブジェクトのインターフェイス
description: オーディオ ミニポート オブジェクトのインターフェイス
ms.assetid: 2e79ad90-fecc-47a7-b487-809325a16239
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f9ddbbfe9e7b36676bf706c5d304d589c0668db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331452"
---
# <a name="audio-miniport-object-interfaces"></a>オーディオ ミニポート オブジェクトのインターフェイス


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ミニポート オブジェクトのインターフェイスについて説明します。 これには次のものがあります。

-   **IMiniport**、他のすべてのオーディオ ミニポート オブジェクト インターフェイスの派生元の基本型であります。

-   オーディオ ミニポート オブジェクト Dmu、MIDI、トポロジ、WaveCyclic、WavePci および WaveRT ミニポート ドライバー インターフェイスを提供します (を参照してください[デバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff538398)) から派生する**IMiniport**

オーディオ ミニポート オブジェクトのインターフェイスは、ミニポート ドライバーがポート ドライバーに提示する主なインターフェイスです。 アダプターのドライバーでは、そのデバイスのポートおよびミニポートのドライバーをまとめてバインドすることによって、オーディオ デバイスの KS フィルターを形成します。 オーディオ ポート オブジェクトの呼び出し、割り当てを行う[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)メソッドとオーディオ ミニポート オブジェクトへの参照を呼び出しのパラメーターとして渡します。 コード例で[サブデバイス作成](https://msdn.microsoft.com/library/windows/hardware/ff538390)このプロセスを示しています。

このセクションでは、次のオーディオ ミニポート オブジェクト インターフェイスについて説明します。

[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)

[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)

[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)

[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)

[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)

 

 





