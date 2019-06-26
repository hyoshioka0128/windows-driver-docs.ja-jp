---
title: オーディオ ポート オブジェクトのインターフェイス
description: オーディオ ポート オブジェクトのインターフェイス
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df7b91e6fafc30108846aab2a161572a61f89d45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355683"
---
# <a name="audio-port-object-interfaces"></a>オーディオ ポート オブジェクトのインターフェイス


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ポート オブジェクトのインターフェイスについて説明します。 これには次のものがあります。

-   **IPort**、他のすべてのオーディオ ポート オブジェクト インターフェイスの派生元の基本型であります。

-   オーディオ ポート オブジェクトの Dmu、MIDI、トポロジ、WaveCyclic、WavePci および WaveRT ポート ドライバー インターフェイスを提供します (を参照してください[デバイスをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)) から派生する**IPort**

オーディオ ポート オブジェクトのインターフェイスは、ポート ドライバーは、ミニポート ドライバーに提示する主なインターフェイスです。 アダプターのドライバーでは、そのデバイスのポートおよびミニポートのドライバーをまとめてバインドすることによって、オーディオ デバイスの KS フィルターを形成します。 オーディオ ポート オブジェクトの呼び出し、割り当てを行う[ **iport::init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)メソッドとオーディオ ミニポート オブジェクトへの参照を呼び出しのパラメーターとして渡します。 コード例で[サブデバイス作成](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)このプロセスを示しています。

このセクションでは、次のオーディオ ポート オブジェクトのインターフェイスについて説明します。

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)

[IPortClsPower](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclspower)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwmiregistration)

 

 





