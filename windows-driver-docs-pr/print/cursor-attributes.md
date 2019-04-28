---
title: カーソル属性
description: カーソル属性
ms.assetid: 43646e2a-bc40-430e-ac7e-6fe4cb353309
keywords:
- カーソルの WDK Unidrv 属性します。
- 一般的なプリンター属性 WDK Unidrv、カーソル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4604e051d424401475de3eaee82de64014e087
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365545"
---
# <a name="cursor-attributes"></a>カーソル属性





カーソルの属性は[一般的な印刷属性](general-printing-attributes.md)プリンターのカーソルの特性を指定します。

次の表は、カーソルの属性を一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>AbsXMovesRightOnly でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 このパラメーターは、デバイスが現在の位置を右に移動した絶対移動コマンドのみを受け入れることを指定するに使用されます。 現在の位置の左への移行が必要な場合は、Unidrv 最初キャリッジ リターンを送信送信される絶対コマンドが新しい現在の位置の右側にあるようにします。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>BadCursorMoveInGrxMode</strong></p></td>
<td><p></p>
<a href="lists.md" data-raw-source="[LIST](lists.md)">リスト</a>のラスター グラフィックス モードでの無効なカーソルの動きを表す値。 1 つ以上を指定できます。X_PORTRAIT X_LANDSCAPE Y_PORTRAIT Y_LANDSCAPE</td>
<td><p>任意。 指定されていない場合は、既定値に制限はありません。 たとえば、LIST(X_PORTRAIT) では、縦向きの x 方向の移動は許可されていませんことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CursorXAfterCR</strong></p></td>
<td><p></p>
いずれか:AT_PRINTABLE_X_ORIGIN AT_CURSOR_X_ORIGIN
<p>キャリッジ リターンの後にカーソルの x 位置を示します。</p></td>
<td><p>任意。 既定値は、これは、物理的な AT_CURSOR_X_ORIGIN で指定しない場合、位置は 0。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EjectPageWithFF?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 プリンターがページを取り出すフォーム フィードを使用するかどうかを示します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>LineSpacingMoveUnit</strong></p></td>
<td><p>正の整数値。 CmdSetLineSpacing コマンドの移動単位を指定します。 単位は 1 インチあたりのドットで表されます。 プリンターの行間を移動単位 1/60th は、インチのこのエントリが 60 をする必要があります。</p>
<p>行の間隔の移動単位は、マスター Y 単位に均等に分割する必要がありますに注意してください。</p>
<p>* MaxLineSpacing パラメーターはまだかどうかを独立したマスター ユニット *<strong>LineSpacingMoveUnit</strong>を指定します。</p></td>
<td><p>任意。 既定値は、1 マスターの単位です。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxLineSpacing</strong></p></td>
<td><p>行の最大間隔を y マスター単位で表す数値。</p></td>
<td><p>任意。 指定しない場合、Unidrv は、最大値がないと仮定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>UseSpaceForXMove でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 カーソルの x 方向の動きを実行する空白文字を使用できるかどうかを示します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>TRUE</strong>します。</p>
<p>場合<strong>TRUE</strong>Unidrv 粗い移動のスペースを使用して、fine の null 値が移動します。 場合<strong>FALSE</strong>Unidrv はすべての移動を null 値を使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>XMoveThreshold</strong></p></td>
<td><p>これを超える移動のしきい値を表す x マスター単位での数値<strong>CmdXMoveAbsolute</strong>の代わりに使用する必要があります<strong>CmdXMoveRelLeft</strong>または<strong>CmdXMoveRelRight</strong>.</p></td>
<td><p>任意。 既定値が 0 の場合に指定しない場合、意味<strong>CmdXMoveAbsolute</strong>常に使用する必要があります。 次の 3 つのすべての x 移動コマンドが指定されている場合にのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>XMoveUnit</strong></p></td>
<td><p>1 インチあたりのドット数では、数値は、の対応では最小の水平方向移動プリンターを表すです。 たとえば、次の移動単位は 1/600 インチ、指定した値は 600 です。</p></td>
<td><p>プリンターが水平方向移動をサポートしているかどうかに必要な<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">カーソル コマンド</a>します。 (指定されて場合、計算するときにこの値を含む<a href="master-units.md" data-raw-source="[master units](master-units.md)">ユニットをマスター</a>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveAttributes</strong></p></td>
<td><p></p>
Y 移動属性を示す値のリスト。 1 つ以上を指定できます。FAV_LF (優先 LF 間隔) SEND_CR_FIRST</td>
<td><p>任意。 指定しない場合、属性がないと仮定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YMoveThreshold</strong></p></td>
<td><p>これを超える移動のしきい値を表す y マスター単位での数値<strong>CmdYMoveAbsolute</strong>の代わりに使用する必要があります<strong>CmdYMoveRelLeft</strong>または<strong>CmdYMoveRelRight</strong>.</p></td>
<td><p>任意。 既定値が 0 の場合に指定しない場合、意味<strong>CmdYMoveAbsolute</strong>常に使用する必要があります。 次の 3 つのすべての y 移動コマンドが指定されている場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YMoveUnit</strong></p></td>
<td><p>1 インチあたりのドット数では、数値は、の対応では最小の垂直方向の移動、プリンターを表すです。 たとえば、次の移動単位は 1/600 インチ、指定した値は 600 です。</p></td>
<td><p>プリンターが垂直方向の移動をサポートしているかどうかに必要な<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">カーソル コマンド</a>します。 (指定されて場合、計算するときにこの値を含む<a href="master-units.md" data-raw-source="[master units](master-units.md)">ユニットをマスター</a>)。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




