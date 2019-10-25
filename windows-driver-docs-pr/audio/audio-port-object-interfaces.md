---
title: オーディオ ポート オブジェクトのインターフェイス
description: オーディオ ポート オブジェクトのインターフェイス
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57715d44ef3065b0378b4073210eb33f0133dcd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831347"
---
# <a name="audio-port-object-interfaces"></a>オーディオ ポート オブジェクトのインターフェイス


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


ここでは、オーディオポートオブジェクトインターフェイスについて説明します。 これには次のものがあります。

-   **IPort**(他のすべてのオーディオポートオブジェクトインターフェイスの派生元である基本型)

-   オーディオポートオブジェクトは、DMus、MIDI、トポロジ、WaveCyclic、WavePci、 **Wavert**の各ポートドライバーのインターフェイスを提供します (「[デバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)」を参照してください)。これはから派生したものです。

オーディオポートオブジェクトインターフェイスは、ポートドライバーがミニポートドライバーに提示する主要なインターフェイスです。 アダプタードライバーは、そのデバイスのポートとミニポートドライバーを結合することによって、オーディオデバイスの KS フィルターを形成します。 バインディングは、オーディオポートオブジェクトの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出し、オーディオミニポートオブジェクトへの参照を呼び出しパラメーターとして渡すことによって実現されます。 [サブデバイス作成](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)のコード例では、このプロセスを示しています。

このセクションでは、次のオーディオポートオブジェクトインターフェイスについて説明します。

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortClsPower](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspower)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwmiregistration)

 

 





