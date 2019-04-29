---
title: WDI データ転送
description: このセクションでは、WDI データ転送について説明します。 このセクションでは、次の用語が使用されます。
ms.assetid: DA07E2C2-6478-40DD-AAD8-8ABD2777CA73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0f24cd1218d67c1ea763f4dcbf29e86e572192
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330520"
---
# <a name="wdi-data-transfer"></a>WDI データ転送


このセクションでは、WDI データ転送について説明します。 このセクションでは、次の用語が使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲット WLAN デバイス (ターゲット)</p></td>
<td align="left"><p>物理 NIC</p></td>
</tr>
<tr class="even">
<td align="left"><p>WLAN の仮想デバイス (ポート)</p></td>
<td align="left"><p>仮想 NIC (たとえば、P2P ロール ポートの場合)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI</p></td>
<td align="left"><p>Microsoft の WLAN のコンポーネントです。 これは、ターゲットに依存しないコンポーネントです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="" id="target-interface-layer---til-"></a>対象となるインターフェイス レイヤー (TIL)</p></td>
<td align="left"><p>バスに固有の Api をターゲットとやり取りするターゲット固有のソフトウェア レイヤーです。 DMA チャネルを管理し、バスの抽象化を提供します。 これを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RX マネージャー/RxMgr</p></td>
<td align="left"><p>RxMgr 実行ターゲットにはオフロードされず処理手順を受信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RxEngine</p></td>
<td align="left"><p>RxEngine で、送信とターゲットの間のデータ同期メッセージを受信および RX 記述子の形式を解釈、および RX DMA のソフトウェアに直接ハードウェアのバッファーを管理します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p> TX マネージャー/TxMgr</p></td>
<td align="left"><p>TX フレームをオペレーティング システムから取得する WDI に準拠したドライバー コンポーネントは、TxEngine に適切な時に、配信し、完了した TX フレームをオペレーティング システムに返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p> TxEngine</p></td>
<td align="left"><p>ホストから、ターゲットに送信データ転送を処理し、ターゲットからの送信完了メッセージを処理するターゲット固有のソフトウェア コンポーネント。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>対象となる抽象化レイヤー (ですか?)</p></td>
<td align="left"><p>「下-エッジ」を持つ WDI 準拠のドライバーに標準化された API が、ターゲット固有の内部実装します。 話しては TxEngine RxEngine などの個々 のターゲット固有のホスト ソフトウェア コンポーネントのコンテナー レイヤーです。</p></td>
</tr>
</tbody>
</table>

 

 

 





