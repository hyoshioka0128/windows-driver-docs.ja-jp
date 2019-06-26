---
title: オペレーティング システムによるミニポート ドライバーの種類
description: オペレーティング システムによるミニポート ドライバーの種類
ms.assetid: 6ab0e4e4-5118-4df5-ba4e-7da66ce5880d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc014ba43a91072abf13884d64844e9255f2d96a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355354"
---
# <a name="miniport-driver-types-by-operating-system"></a>オペレーティング システムによるミニポート ドライバーの種類


オーディオ ドライバーを開発する際に、ドライバーは PortCls システム ドライバー (Portcls.sys) または AVStream クラスのシステム ドライバーと共に動作するかどうかを判断する必要があります。 ビデオ ストリームが必要でない場合は、PortCls システム ドライバーで動作するドライバーを必要があります。 これら 2 つの種類のシステム ドライバーの詳細については、次を参照してください。、[ポート クラスの概要](introduction-to-port-class.md)と[AVStream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)トピック。

PortCls システム ドライバー (Portcls.sys) では、レンダリング、wave と MIDI ストリームをキャプチャするオーディオ デバイスをサポートするためにいくつかの組み込みのポート ドライバーを提供します。 通常、ポート ドライバーは、オーディオ サブデバイスの各クラスの機能の大半を提供します。

各ポート ドライバーは、ミニポート ドライバーと組み合わせて動作します。 ミニポート ドライバーでは、wave レンダリングまたは wave キャプチャ デバイスのハードウェアに依存する関数を管理します。 つまり、ミニポート ドライバーでは、サード パーティ製のオーディオ デバイスのハードウェアに固有の機能のサポートを提供します。

開発するミニポート ドライバーの種類は、ターゲットの Windows オペレーティング システムと、オーディオ デバイスによって提供される機能によって決まります。 次の表では、ミニポート ドライバーおよびそれらをサポートする Windows オペレーティング システムのさまざまな種類を示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ミニポート ドライバー</th>
<th align="left">Windows XP</th>
<th align="left">Windows Vista</th>
<th align="left">Windows 7</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wavecyclic-miniport-driver.md" data-raw-source="[WaveCyclic](wavecyclic-miniport-driver.md)">WaveCyclic</a></p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wavepci-miniport-driver.md" data-raw-source="[WavePci](wavepci-miniport-driver.md)">WavePci</a></p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wavert-miniport-driver.md" data-raw-source="[WaveRT](wavert-miniport-driver.md)">WaveRT</a></p></td>
<td align="left"></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="topology-miniport-driver.md" data-raw-source="[Topology](topology-miniport-driver.md)">トポロジ</a></p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="midi-miniport-driver.md" data-raw-source="[MIDI](midi-miniport-driver.md)">MIDI</a></p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="dmus-miniport-driver.md" data-raw-source="[DMus](dmus-miniport-driver.md)">Dmu</a></p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
<td align="left"><p>○</p></td>
</tr>
</tbody>
</table>

 

各ポート ドライバーでは、ミニポート ドライバーには、インターフェイスを実装します。 ポート ドライバーとの通信、ミニポート ドライバーもインターフェイスを実装する必要があります。 ミニポート ドライバーによって実装されるインターフェイスの詳細については、次を参照してください。[ミニポート インターフェイス](miniport-interfaces.md)します。

**注**  オーディオ ドライバーを Windows Vista およびそれ以降のオペレーティング システムを開発する場合、次の把握してあります。
-   WaveCyclic - または、WavePci のロゴ認定を取得できません-オーディオ ドライバーのベースします。

-   Dmu のカーネル モードのソフトウェアのシンセサイザーのサポートはありません。 ただし、MIDI I/O ハードウェアのサポートが提供されます。

 

 

 




