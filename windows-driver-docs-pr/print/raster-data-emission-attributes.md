---
title: ラスター データ出力属性
description: ラスター データ出力属性
ms.assetid: 98366b64-f96b-4275-ba25-8483abf705aa
keywords:
- データ出力ラスター印刷 WDK Unidrv を属性します。
- 出力のラスター印刷 WDK Unidrv を属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8351112bd3860494a3823205f3f5021a5927ee9d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349947"
---
# <a name="raster-data-emission-attributes"></a>ラスター データ出力属性





次の表は、ラスター データの出力に対するプリンターのサポートを記述する属性を一覧表示します。

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
<td><p><em><strong>CursorXAfterSendBlockData</strong></p></td>
<td><p>ラスターのデータのブロックが送信された後、カーソルの x 位置を示す定数値。 いずれかを指定できます。</p>
AT_GRXDATA_END AT_GRXDATA_ORIGIN AT_CURSOR_X_ORIGIN がグラフィックス ブロック、ブロック、またはカーソルのオリジン内の最後の 1 つ後のピクセルの開始時のピクセルを意味します。</td>
<td><p>任意。 指定しない場合、既定値は AT_GRXDATA_END にします。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterSendBlockData</strong></p></td>
<td><p>ラスターのデータのブロックが送信された後、カーソルの y 位置を示す定数値。 いずれかを指定できます。</p>
NO_MOVE AUTO_INCREMENT</td>
<td><p>任意。 指定しない場合、既定値は NO_MOVE、つまりカーソルの y 位置は変更にします。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxMultipleRowBytes</strong></p></td>
<td><p>ラスター設定デバイスにデータをダウンロードするときに使用するラスターの最大サイズのブロックを表す数値を指定 * SendMultipleRows でしょうか。<strong>TRUE</strong>します。</p></td>
<td><p>既定値は、32 KB です。 最大許容値は 256 KB です。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MirrorRasterByte</strong>でしょうか。</p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示すかどうか Unidrv を (逆方向) にミラー イメージ データの各バイト。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MirrorRasterPage でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、出力はミラー化する、かどうか。 ときに<strong>TRUE</strong>ラスター、として印刷したり、縞模様から反対方向でミラー化し、ページで、この属性が原因すべて。 つまり、縦ページは、右に左ミラーリング横向きのページでは、ミラー化された上から下へです。</p>
<p>この属性は透明または背面印刷フィルムの印刷時に最も適しています。</p></td>
<td><p>任意。 既定値は<strong>FALSE</strong>します。</p>
<p>この属性は、グローバル属性を再配置することです。 ルート レベルの属性として表示される (を参照してください<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 属性</a>) と構成の依存関係が存在しないか、ように思われる場合 * オプションまたは * の場合は、メディアの種類ごとに構築します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MoveToX0BeforeSetColor でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、明示的な色の選択コマンドを送信する前に 0 に設定する必要があります、カーソルの x 座標のかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 <strong>TRUE</strong>場合にのみ<em> <strong>UseExpColorSelectCmd でしょうか。</strong>も<strong>TRUE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OptimizeLeftBound でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示す各バンドのバインド Unidrv が左側にある空白を削除するかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>OutputDataFormat</strong></p></td>
<td><p>H_BYTE または V_BYTE、データのバイトのビットがピクセルが水平方向または垂直方向のピクセルにマップされているかどうかを示します。</p></td>
<td><p>任意。 指定しない場合、既定値は H_BYTE にします。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PreAnalysisOptions</strong></p></td>
<td><p>数値 0、1、2、4、または 8 のいずれかです。</p>
<p>各属性のパラメーターの意味については、次を参照してください。 <a href="preanalysis-infrastructure.md" data-raw-source="[Preanalysis Infrastructure](preanalysis-infrastructure.md)">Preanalysis インフラストラクチャ</a>します。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>RasterSendAllData でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、Unidrv が空白のスキャン ラインとスキャン ライン内の空白を含む、すべてのラスター データを送信するかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>SendMultipleRows でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、一度に 1 つブロック CmdSendBlockData で指定されたコマンドが複数送信できるかどうか。</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><em><strong>StripBlanks</strong></p></td>
<td><p>ラスターのデータ ブロックが空白のリストを削除する必要があります。 1 つ以上を指定できます。</p>
先頭、末尾に含まれています。</td>
<td><p>任意。 指定しない場合、Unidrv は任意の空白を削除できません。 参照してください *<strong>MinStripBlankPixels</strong>で<a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解決の機能のオプション属性</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>UseExpColorSelectCmd でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>プリンターに明示的な色選択コマンドが必要とするかどうかを示す色ラスター データから分離します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 ドット マトリックスのプリンターの値を必要と<strong>TRUE</strong>します。</p></td>
</tr>
</tbody>
</table>

 

ラスターのデータの出力に関連付けられているコマンドについては、次を参照してください。[ラスター データ出力コマンド](raster-data-emission-commands.md)します。

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




