---
title: ミニポート インターフェイス
description: ミニポート インターフェイス
ms.assetid: 50b92adc-a63c-4242-9ec9-4d97151f0f91
keywords:
- オーディオミニポートドライバー WDK、インターフェイス
- ミニポートドライバー WDK オーディオ、インターフェイス
- ミニポートインターフェイス WDK オーディオ
- ポートクラスドライバー WDK オーディオ
- PortCls WDK audio, インターフェイス
- インターフェイス WDK オーディオ
- 組み込みのポートドライバー WDK オーディオ
- stream インターフェイスの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171d0991ee2198be71c2ec16b8a1464b462169bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832569"
---
# <a name="miniport-interfaces"></a>ミニポート インターフェイス


## <span id="miniport_interfaces"></span><span id="MINIPORT_INTERFACES"></span>


「[デバイスのサポート](supporting-a-device.md)」で説明されているように、PortCls システムドライバーには、WAVE および MIDI デバイスを管理するための一連の組み込みのポートドライバーが用意されています。 これらのポートドライバーのいずれかを使用して特定の種類のオーディオデバイスを管理するには、アダプタードライバーが、デバイスのハードウェアに依存するすべての機能を管理することで、ポートドライバーを補完する対応するミニポートドライバーを提供する必要があります。

このセクションでは、次のミニポートドライバーの種類について説明します。

[WaveRT ミニポートドライバー](wavert-miniport-driver.md)

オーディオデータ用の循環バッファーを使用する wave レンダリングまたはキャプチャデバイスのハードウェアに依存する機能を管理することによって、WaveRT ポートドライバーを補完します。

[トポロジミニポートドライバー](topology-miniport-driver.md)

オーディオアダプターのミキサー回路にあるさまざまなハードウェア制御 (ボリュームレベルなど) を管理することによって、トポロジポートドライバーを補完します。

[MIDI ミニポートドライバー](midi-miniport-driver.md)

単純な MIDI デバイスのハードウェアに依存する機能を管理することによって、MIDI ポートドライバーを補完します。

[DMus ミニポートドライバー](dmus-miniport-driver.md)

高度な MIDI デバイスのハードウェアに依存する機能を管理して、DMus ポートドライバーを補完します。

各ポートドライバーは**Iportxxx**インターフェイスを実装し、これはミニポートドライバーに提供されます。 さらに、ミニポートドライバーは、ポートドライバーがミニポートドライバーとの通信に使用する**IMiniportXxx**インターフェイスを実装する必要があります。 次の表は、 **Iportxxx**インターフェイスと、各デバイスの種類に対応する**IMiniportXxx**インターフェイスを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスの種類</th>
<th align="left">ポートドライバーインターフェイス</th>
<th align="left">ミニポートドライバーインターフェイス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WaveCyclic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic" data-raw-source="[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic" data-raw-source="[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)" data-raw-source="[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))">IPortWavePci</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci" data-raw-source="[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert" data-raw-source="[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert" data-raw-source="[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>トポロジ</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology" data-raw-source="[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)">IPortTopology</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology" data-raw-source="[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi" data-raw-source="[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)">IPortMidi</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi" data-raw-source="[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus" data-raw-source="[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)">IPortDMus</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus" data-raw-source="[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

上の表では、すべての**Iportxxx**インターフェイスが基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)から派生し、すべての**IMiniportXxx**インターフェイスが[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)から派生しています。

 

 




