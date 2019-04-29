---
title: デバイス フォントの属性
description: デバイス フォントの属性
ms.assetid: 748faa90-9c31-44c2-8bb3-641a1f95eab1
keywords:
- デバイス フォント WDK Unidrv
- フォントの WDK Unidrv 属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ac6cd84875d3e93fb22f5b9a4524d5141eb000
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331186"
---
# <a name="attributes-for-device-fonts"></a>デバイス フォントの属性





次の表は、デバイスのフォントのプリンターのサポートを記述する属性を一覧表示します。

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
<td><p><strong><em>CharPosition</strong></p></td>
<td><p>べき矩形または基準。 境界ボックスの文字を印刷する前に印刷ヘッドを配置する文字の領域を示します。</p></td>
<td><p>任意。 指定しない場合、既定値はべき矩形にします。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>DefaultCTT</strong></p></td>
<td><p>既定の文字変換テーブルの RC_CTT リソース識別子を表す数値。</p></td>
<td><p></p>
任意。 TTY プリンターにのみ適用されます。
指定しない場合、変換テーブルはありません。 (この属性は、GPC ファイルの旧バージョンとの互換性のためだけに提供されます)。</td>
</tr>
<tr class="odd">
<td><p><strong><em>DefaultFont</strong></p></td>
<td><p>既定のフォントの RC_FONT または RC_UFM リソース識別子を表す数値。</p></td>
<td><p>デバイス フォントをプリンターがサポートしているかが必要です。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>LookAheadRegion</strong></p></td>
<td><p>どの程度進んでドライバーを表す数値 (整数) の値は、テキストを出力するかどうかを判断する「検索」する必要があります。 この値は<em>y</em>マスターの単位がピクセル数は整数に変換できる必要があります。 詳細については、次の表に続くコメントを参照してください。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。 テキストおよびビットマップ データを並べ替えるために、シリアル プリンター、(たとえば、HP DeskJet) でのみ使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontUsePerPage</strong></p></td>
<td><p>フォントの最大数を表す数値 1 ページあたりのプリンターを使用できます。</p></td>
<td><p>任意。 指定しない場合、制限はありません。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextYOffset</strong></p></td>
<td><p>垂直方向の距離を表す数値<em>y</em>マスターの単位にビットマップのフォントの基準に合うように、フォントを移動する必要があります。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。 (ドット マトリックスの一部のプリンターで使用)。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

### <a href="" id="note-on--lookaheadregion"></a>Note on \*LookAheadRegion

先読み領域のサイズを決定するプリンター ドライバーが現在のスキャン ラインの値に基づく追加を実行する必要があります、 \* **LookAheadRegion**属性。 スキャン ラインが中にピクセル単位であるため\* **LookAheadRegion**ユニットを垂直方向のマスターでは、ドライバーは、属性の値をピクセルに変換する必要があります。

たとえば場合の値、 \* **LookAheadRegion**属性が 600 がある垂直マスター ユニットを 1 インチあたり 1200 先読み領域に 0.5 インチのサイズ。 現在の解像度が 300 dpi の場合は、0.5 インチが 150 ピクセル (垂直) または 150 のスキャン ラインに対応しています。 プリンターは、スキャン ライン 100 では現在場合、ドライバー テキストのベースライン スキャン 100 ~ 行 250 検索する必要があります。

ドライバーでは、1 回だけ見つかったテキストが出力されますが、各スキャン ラインのこのプロセスが繰り返されます。

 

 




