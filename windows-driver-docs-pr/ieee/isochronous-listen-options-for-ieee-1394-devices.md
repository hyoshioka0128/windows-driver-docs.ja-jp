---
title: IEEE 1394 デバイス アイソクロナス リッスン オプション
description: IEEE 1394 デバイス アイソクロナス リッスン オプション
ms.assetid: a369b7f0-be85-49f0-bb09-d07cbd3d3558
keywords:
- アイソクロナス I/O WDK の IEEE 1394 バス、リッスン オプション
- WDK の IEEE 1394 のオプションのバスをリッスンします。
- DMA WDK の IEEE 1394 のバスのパケットに基づく
- ストリーム ベースの DMA WDK の IEEE 1394 バス
- DMA が IEEE 1394 の WDK を転送します。
- WDK IEEE 1394 の DMA パケット
- パケット ヘッダーの削除
- WDK の IEEE 1394 ヘッダー バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f3a23f2d45c6d8b7f24114b059ef599cc3901c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560721"
---
# <a name="isochronous-listen-options-for-ieee-1394-devices"></a>IEEE 1394 デバイス アイソクロナス リッスン オプション





このセクションでは、アイソクロナス リッスンのさまざまなオプションについて説明します。

### <a name="receiving-or-stripping-packet-headers"></a>受信またはパケット ヘッダーの削除

ホスト コント ローラーは、自動的にオフ アイソクロナスのパケット ヘッダーを取り除きます可能性がありますいません。 バス ドライバーの設定、ホスト\_情報\_サポート\_RETURNING\_ISO\_HDR フラグの**HostCapabilities**のメンバー、 [**取得\_ローカル\_ホスト\_情報 2** ](https://msdn.microsoft.com/library/windows/hardware/ff537147)場合は、ホスト コント ローラーを構造体*いない*アイソクロナス パケットからヘッダーを自動的に削除します。

また、ホスト コント ローラーがヘッダーの構成可能な削除をサポートすることがあります。 バス ドライバーの設定、ホスト\_情報\_サポート\_アイソクロナス\_HostCapabilities ホスト コント ローラーを構成して、ヘッダーを削除する場合の STRIPPING フラグ。 ドライバーの送信ヘッダーを削除するホスト コント ローラーで実際に構成する、 [**要求\_アイソクロナス\_ALLOCATE\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)リソースに要求\_ストリップ\_追加\_QUADLETS フラグを設定します。 **NQuadletsToStrip**メンバーは、各パケットの先頭を取り除く quadlets の数を指定します。 たとえば、 **nQuadletsToStrip** = 1 は isochronous パケット ヘッダーを取り除きます。

### <a name="stream-versus-packet-based-dma"></a>パケットに基づく DMA と Stream

ストリームおよびパケット ベース DMA 戦略では、基になるホスト コント ローラーからのサポートが必要です。 すべてのホスト コント ローラーは DMA の戦略の少なくとも 1 つをサポートし、準拠 OHCI ホスト コント ローラーは、両方をサポートします。

パケットに基づく DMA と DMA のストリーム ベースのすべてのパケットが同じサイズの場合と同様の特性があります。 パケット サイズが異なる場合に、DMA の 2 つの並べ替えによって大きく異なる特性があります。

DMA のストリーム ベースのホスト コント ローラーは、書き込まれているデータのギャップを残さず、I/O バッファーを塗りつぶすようにパケットの境界を無視します。 特定のパケットの場所を決定するためには、前のすべてのパケットの長さが必要です。

パケットに基づくの DMA では、ホスト コント ローラーは、バッファーごとの 1 つだけの isochronous パケットを書き込みます。 したがってパケットのモードでホスト コント ローラー行間を書き込むデータ パケットの最大サイズの整数倍である I/O バッファーの先頭からの距離を各パケットから開始できるようにします。 特定のパケットが、最大値よりも小さい場合は、そのパケットの末尾と次のパケットの間にあるデータは定義されません。 したがってパケットが最大サイズよりも小さい場合は、バッファーに空き無駄になります。 たとえば、10 パケットを常に保持するために十分な大きさのバッファーは、いくつかのパケットが許容される最大サイズよりも小さい場合でも、正確に 10 個のパケットを保持します。

選択する DMA モードに関係なく、いくつかの設計上のトレードオフが適用されます。 たとえば、バッファー サイズの選択では、DMA モードを使用して、デバイスのパフォーマンスに影響します。 ラージ バッファーは、いくつかのバッファーの数が多いの初期化に関連するオーバーヘッドを回避するために、効率性を提供します。 また、少ないバッファー少ない DMA 記述子が必要なことを意味します。 その一方より大きいバッファーが I/O 操作の開始と、バス ドライバー関数からドライバーに通知バッファーがいっぱいである時点までの待機時間を増やします。

ホスト コント ローラーは、DMA の両方の種類をサポートする場合、バス ドライバーは、既定値のストリーム ベースの DMA ホスト コント ローラーを設定します。 ホスト コント ローラーをパケットに基づく DMA をリセットするドライバーが、リソースを設定します。\_使用\_パケット\_リソース ハンドルを割り当てるときに基づくフラグ。

ドライバーを使用して、 [**要求\_取得\_ローカル\_ホスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537644) bus 要求 (で、 **u.GetLocalHostInformation.nLevel** 、IRB のメンバー = GET\_ホスト\_機能) ホスト コント ローラーの特性を判断します。 バス ドライバーを返します、 [**取得\_ローカル\_ホスト\_情報 2** ](https://msdn.microsoft.com/library/windows/hardware/ff537147)構造、および内のフラグの設定、 **HostCapabilities**ホスト コント ローラーのサポートを示すメンバー:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DMA の種類</th>
<th>HostCapabilities フラグ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ストリーム ベース</p></td>
<td><p>HOST_INFO_STREAM_BASED</p></td>
</tr>
<tr class="even">
<td><p>パケットに基づく</p></td>
<td><p>HOST_INFO_PACKET_BASED</p></td>
</tr>
</tbody>
</table>

 

 

 




