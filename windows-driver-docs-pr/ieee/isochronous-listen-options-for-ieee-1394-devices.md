---
title: IEEE 1394 デバイスの等時性リッスンのオプション
description: IEEE 1394 デバイスの等時性リッスンのオプション
ms.assetid: a369b7f0-be85-49f0-bb09-d07cbd3d3558
keywords:
- アイソクロナス i/o WDK IEEE 1394 bus、listen オプション
- リッスンオプション WDK IEEE 1394 バス
- パケットベースの DMA WDK IEEE 1394 バス
- ストリームベースの DMA WDK IEEE 1394 バス
- DMA 転送 WDK IEEE 1394 バス
- パケット DMA WDK IEEE 1394 バス
- パケットヘッダーの除去
- ヘッダー WDK IEEE 1394 bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9513cfa80bc544cf444266d5c6add3924858b2d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841536"
---
# <a name="isochronous-listen-options-for-ieee-1394-devices"></a>IEEE 1394 デバイスの等時性リッスンのオプション





このセクションでは、さまざまなアイソクロナスリッスンオプションについて説明します。

### <a name="receiving-or-stripping-packet-headers"></a>パケットヘッダーの受信または削除

ホストコントローラーは、アイソクロナスパケットのヘッダーを自動的に削除しない場合があります。 バスドライバーは、ホストコントローラーがある場合に、 [**GET\_LOCAL\_HOST\_INFO2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2)構造体の**hostcapabilities**メンバーの\_ISO\_HDR フラグを返す\_をサポート\_\_情報を設定します。アイソクロナスパケットのヘッダーは自動的に削除*されません*。

また、ホストコントローラーは、構成可能なヘッダーの削除をサポートする場合があります。 バスドライバーは、ホストコントローラーがヘッダーを削除するように構成できる場合、ホスト\_情報\_\_ISOCH\_削除フラグをサポートします。 ヘッダーを削除するようにホストコントローラーを構成するには、ドライバーが\_要求を送信して、リソース\_ストリップ\_追加の\_QUADLETS ISOCH フラグが設定された[ **\_リソースの要求\_割り当て**](https://msdn.microsoft.com/library/windows/hardware/ff537649)ます。 **NQuadletsToStrip**メンバーは、各パケットの先頭から除去する quadlets の数を指定します。 たとえば、 **nQuadletsToStrip** = 1 の場合、アイソクロナスパケットヘッダーが削除されます。

### <a name="stream-versus-packet-based-dma"></a>ストリームとパケットベースの DMA

ストリームベースおよびパケットベースの DMA 戦略では、基になるホストコントローラーからのサポートが必要です。 すべてのホストコントローラーは、少なくとも1つの DMA 戦略をサポートし、OHCI 準拠のホストコントローラーは両方をサポートします。

パケットベースの DMA とストリームベースの DMA の特性は、すべてのパケットが同じサイズである場合に似ています。 ただし、パケットサイズが変化する場合、2種類の DMA の特性は大きく異なります。

ストリームベースの DMA では、ホストコントローラーは i/o バッファーがいっぱいになったときにパケット境界を無視し、書き込まれたデータにギャップが生じないようにします。 特定のパケットの場所を特定するには、以前のすべてのパケットの長さを把握している必要があります。

パケットベースの DMA では、ホストコントローラーはバッファーごとに1つのアイソクロナスパケットだけを書き込みます。 したがって、パケットモードでは、ホストコントローラーは書き込み対象のデータをスペースとして格納します。これにより、各パケットは、最大パケットサイズの整数倍の i/o バッファーの先頭からの距離で開始されます。 特定のパケットが最大値より小さい場合、そのパケットの末尾と次のパケットの開始位置の間にあるデータは未定義になります。 パケットが最大サイズより小さい場合は、一部のバッファー領域が無駄になります。 たとえば、10個のパケットを保持するのに十分な大きさのバッファーは、許可されている最大サイズよりも小さいパケットがある場合でも、常に10個のパケットを保持します。

選択する DMA モードに関係なく、いくつかの設計上のトレードオフが適用されます。 たとえば、バッファーサイズの選択は、使用する DMA モードに関係なく、デバイスのパフォーマンスに影響します。 大きなバッファーを使用すると、大量のバッファーの初期化に関連するオーバーヘッドの一部を回避できるため、効率が向上します。 また、バッファーが減ることは、必要な DMA 記述子が減ることを意味します。 一方、大きなバッファーを使用すると、i/o 操作の開始から、バスドライバーがバッファーがいっぱいであることを関数ドライバーに通知する瞬間までの待機時間が増加します。

ホストコントローラーで両方の種類の DMA がサポートされている場合、バスドライバーは、既定のストリームベースの DMA にホストコントローラーを設定します。 ホストコントローラーをパケットベースの DMA にリセットするには、ドライバーがリソースハンドルを割り当てるときに\_パケット\_ベースのフラグを使用\_ようにリソースを設定する必要があります。

ドライバーは、要求を使用して[ **\_ローカル\_ホスト\_情報バス要求\_取得**](https://msdn.microsoft.com/library/windows/hardware/ff537644)します。この要求は、IRB = GET\_HOST\_の機能の**n レベル**のメンバーであり、ホストコントローラー。 バスドライバーは、 [**GET\_ローカル\_ホスト\_INFO2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2)構造体を返し、 **hostcapabilities**メンバー内にフラグを設定して、ホストコントローラーがサポートする内容を示します。

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
<td><p>ストリームベース</p></td>
<td><p>HOST_INFO_STREAM_BASED</p></td>
</tr>
<tr class="even">
<td><p>パケットベース</p></td>
<td><p>HOST_INFO_PACKET_BASED</p></td>
</tr>
</tbody>
</table>

 

 

 




