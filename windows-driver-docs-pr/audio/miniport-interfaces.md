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
ms.openlocfilehash: b66c0cef0e2ca0e50e8f95f7fd6a8ed307ff69cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558648"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536899" data-raw-source="[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536714" data-raw-source="[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536905" data-raw-source="[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)">IPortWavePci</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536724" data-raw-source="[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536920" data-raw-source="[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536737" data-raw-source="[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>トポロジ</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536896" data-raw-source="[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)">IPortTopology</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536712" data-raw-source="[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536891" data-raw-source="[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)">IPortMidi</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536703" data-raw-source="[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536879" data-raw-source="[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)">IPortDMus</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536699" data-raw-source="[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

前の表では、すべて**IPortXxx**基底インターフェイスから派生したインターフェイスは[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)、およびすべて**IMiniportXxx**インターフェイスから派生[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)します。

 

 




