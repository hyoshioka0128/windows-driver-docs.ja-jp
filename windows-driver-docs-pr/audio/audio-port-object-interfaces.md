---
title: オーディオ ポート オブジェクト インターフェイス
description: オーディオ ポート オブジェクト インターフェイス
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40abbf4a9f00d2492da8106a2b40d0c5b9ee17f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537970"
---
# <a name="audio-port-object-interfaces"></a>オーディオ ポート オブジェクト インターフェイス


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ポート オブジェクトのインターフェイスについて説明します。 これには次のものがあります。

-   **IPort**、他のすべてのオーディオ ポート オブジェクト インターフェイスの派生元の基本型であります。

-   オーディオ ポート オブジェクトの Dmu、MIDI、トポロジ、WaveCyclic、WavePci および WaveRT ポート ドライバー インターフェイスを提供します (を参照してください[デバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff538398)) から派生する**IPort**

オーディオ ポート オブジェクトのインターフェイスは、ポート ドライバーは、ミニポート ドライバーに提示する主なインターフェイスです。 アダプターのドライバーでは、そのデバイスのポートおよびミニポートのドライバーをまとめてバインドすることによって、オーディオ デバイスの KS フィルターを形成します。 オーディオ ポート オブジェクトの呼び出し、割り当てを行う[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)メソッドとオーディオ ミニポート オブジェクトへの参照を呼び出しのパラメーターとして渡します。 コード例で[サブデバイス作成](https://msdn.microsoft.com/library/windows/hardware/ff538390)このプロセスを示しています。

このセクションでは、次のオーディオ ポート オブジェクトのインターフェイスについて説明します。

[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)

[IPortClsPower](https://msdn.microsoft.com/library/windows/hardware/ff536844)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)

[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)

[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)

[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)

[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)

[IPortWMIRegistration](https://msdn.microsoft.com/library/windows/hardware/ff536935)

 

 





