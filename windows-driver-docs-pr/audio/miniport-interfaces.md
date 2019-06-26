---
title: ミニポート インターフェイス
description: ミニポート インターフェイス
ms.assetid: 50b92adc-a63c-4242-9ec9-4d97151f0f91
keywords:
- オーディオのミニポート ドライバー WDK、インターフェイス
- ミニポート ドライバー WDK のオーディオ、インターフェイス
- ミニポート インターフェイス WDK オーディオ
- ポート クラス ドライバー WDK オーディオ
- PortCls WDK オーディオ、インターフェイス
- インターフェイスの WDK オーディオ
- 組み込みのポート ドライバー WDK オーディオ
- ストリーム インターフェイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05a51cab5a86d874bc172190782434e6a20aa86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363212"
---
# <a name="miniport-interfaces"></a>ミニポート インターフェイス


## <span id="miniport_interfaces"></span><span id="MINIPORT_INTERFACES"></span>


」の説明に従って[デバイスをサポートしている](supporting-a-device.md)、PortCls システム ドライバーは、wave および MIDI デバイスを管理するため、一連の組み込みのポートのドライバーを提供します。 これらのポート ドライバーのいずれかを使用して、特定の種類のオーディオ デバイスを管理する、アダプタのドライバはすべてのデバイスのハードウェアに依存する関数を管理することで、ポートのドライバーを補完する、対応するミニポート ドライバーを提供する必要があります。

このセクションでは、次のミニポート ドライバーの種類について説明します。

[WaveRT ミニポート ドライバー](wavert-miniport-driver.md)

オーディオ データの循環バッファーを使用して wave レンダリングまたはキャプチャ デバイスのハードウェアに依存する機能を管理することによって、WaveRT ポート ドライバーを補完します。

[トポロジのミニポート ドライバー](topology-miniport-driver.md)

アダプターのオーディオ ミキサー回路でさまざまなハードウェア コントロール (たとえば、ボリューム レベル) を管理することによってトポロジ ポート ドライバーを補完します。

[MIDI ミニポート ドライバー](midi-miniport-driver.md)

単純な MIDI デバイスのハードウェアに依存する機能を管理することによって、MIDI ポート ドライバーを補完します。

[Dmu ミニポート ドライバー](dmus-miniport-driver.md)

補完、Dmu は、高度な MIDI デバイスのハードウェアに依存する関数を管理することで、ドライバーを移植します。

各ポート ドライバーは、実装、 **IPortXxx**インターフェイスで、ミニポート ドライバーに表示します。 さらに、ミニポート ドライバーを実装する必要があります、 **IMiniportXxx**インターフェイスで、ミニポート ドライバーとの通信にポート ドライバーを使用します。 次の表は、 **IPortXxx**インターフェイスと、対応する**IMiniportXxx**各デバイスの種類のインターフェイス。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスの種類</th>
<th align="left">ポート ドライバー インターフェイス</th>
<th align="left">ミニポート ドライバー インターフェイス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WaveCyclic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic" data-raw-source="[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic" data-raw-source="[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)" data-raw-source="[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))">IPortWavePci</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci" data-raw-source="[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert" data-raw-source="[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert" data-raw-source="[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>トポロジ</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology" data-raw-source="[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)">IPortTopology</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology" data-raw-source="[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi" data-raw-source="[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)">IPortMidi</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi" data-raw-source="[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus" data-raw-source="[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)">IPortDMus</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus" data-raw-source="[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

前の表では、すべて**IPortXxx**基底インターフェイスから派生したインターフェイスは[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)、およびすべて**IMiniportXxx**インターフェイスから派生[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)します。

 

 




