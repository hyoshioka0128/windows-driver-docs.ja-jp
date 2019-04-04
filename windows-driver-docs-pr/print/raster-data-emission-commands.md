---
title: ラスター データ出力コマンド
description: ラスター データ出力コマンド
ms.assetid: 31a25de3-f66b-4cf0-90ea-988d75838f68
keywords:
- データ出力ラスター印刷コマンド WDK Unidrv
- 出力のラスター印刷コマンド WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd12851f90f20be054259775302005204fe20981
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530079"
---
# <a name="raster-data-emission-commands"></a>ラスター データ出力コマンド





次の表には、ラスター データの出力に対するコマンドが表示されます。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CmdBeginRaster</p></td>
<td><p>ラスターのデータ転送を開始するコマンド。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv は初期化が不要と仮定します。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndRaster</p></td>
<td><p>ラスターのデータ転送を完了するコマンドです。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv 転送完了操作は必要ありません前提としています。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetDestBmpHeight</p></td>
<td><p>コピー先のビットマップの高さを設定するコマンドです。</p></td>
<td><p>(省略可能)。 プリンターがスケーラブルなビットマップをサポートする場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetDestBmpWidth</p></td>
<td><p>コピー先のビットマップの幅を設定するコマンドです。</p></td>
<td><p>(省略可能)。 プリンターがスケーラブルなビットマップをサポートする場合にのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetSrcBmpHeight</p></td>
<td><p>ソース ビットマップの高さを設定するコマンドです。</p></td>
<td><p>(省略可能)。 プリンターがスケーラブルなビットマップをサポートする場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetSrcBmpWidth</p></td>
<td><p>ソース ビットマップの幅を設定するコマンドです。</p></td>
<td><p>(省略可能)。 プリンターがスケーラブルなビットマップをサポートする場合にのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlockData</p></td>
<td><p>データのブロックをプリンターに配信するコマンドです。</p></td>
<td><p>必須。 場合 * OutputDataFormat V_BYTE は、ブロックには、印刷ヘッドの物理パスを 1 つのデータが含まれています。 (を参照してください * PinsPerPhysPass)。 場合 *<strong>OutputDataFormat</strong> H_BYTE は、ブロックには、印刷ヘッドの論理パスを 1 つのデータが含まれています。 (を参照してください * PinsPerLogPass)。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndBlockData</p></td>
<td><p>CmdSendBlockData コマンドを使用して送信されたデータのブロックの終了を示すコマンド。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv では、ブロックの終了を示すコマンドは必要ありません前提としています。 (ドット マトリックスの一部のプリンターで使用)。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendBlackData</p></td>
<td><p>プリンターに黒の背景のデータを提供するコマンドです。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendBlueData</p></td>
<td><p>プリンターに青いプレーン データを提供するコマンドです。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendCyanData</p></td>
<td><p>シアン平面データ、プリンターを配信するコマンド。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendGreenData</p></td>
<td><p>プリンターに緑色のプレーン データを提供するコマンドです。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendMagentaData</p></td>
<td><p>マゼンタ平面データ、プリンターを配信するコマンド。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>CmdSendRedData</p></td>
<td><p>プリンターに赤いプレーン データを提供するコマンドです。</p></td>
<td><p>必要な場合 * UseExpColorSelectCmd でしょうか。属性は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSendYellowData</p></td>
<td><p>プリンターに黄色のプレーン データを提供するコマンドです。</p></td>
<td><p>必要な場合 *<strong>UseExpColorSelectCmd でしょうか。</strong>属性が<strong>FALSE</strong>します。</p></td>
</tr>
</tbody>
</table>

 

例については、、[サンプル GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




