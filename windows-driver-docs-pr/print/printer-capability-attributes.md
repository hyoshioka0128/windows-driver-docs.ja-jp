---
title: プリンター機能属性
description: プリンター機能属性
ms.assetid: 3ee98eee-8f46-4bf0-ac2c-f47f8402fa86
keywords:
- プリンター機能属性 WDK Unidrv
- 一般的なプリンタ属性 WDK Unidrv、プリンタ機能
- 機能属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d281f4aa54f7052de3ff847c284e7d82a556cc81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824338"
---
# <a name="printer-capability-attributes"></a>プリンター機能属性





プリンターの機能属性は、すべての用紙サイズと向きに影響する、ページ余白、回転、およびテキスト印刷機能としてプリンターの特性を指定する[一般的な印刷属性](general-printing-attributes.md)です。

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
<td><p><strong>Memoryusage</strong>の <em></p></td>
<td><p></p>
プリンターメモリに格納されているデータの種類を示す定数の一覧。 1つ以上の: FONT ラスターベクターを指定できます。
<p>データ型が一覧表示されていても、プリンターでサポートされていない場合は、無視されます。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は LIST (FONT、ラスター、VECTOR) です。 詳細については、「<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">プリンターメモリ構成の説明</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>OEMCustomData</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>Iprintoemdriveruni::D rvgetgpddata</strong></a>を呼び出すときに、<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">レンダリングプラグイン</a>に提供される引用符で囲まれたテキスト文字列。</p></td>
<td><p>レンダリングプラグインが<strong>Iprintoemdriveruni::D rvgetgpddata</strong>を呼び出す場合に必要です。</p>
<p>テキスト文字列の内容の解釈は、レンダリングプラグインによって決定されます。</p>
<p>この属性は再配置可能なグローバル属性です。ルートレベル (<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">ルートレベルのみの属性</a>を参照) に配置して、プリンター構成に依存しないことを示します。または、依存関係がある場合は、<em>オプションまたは * ケースコンストラクトと共に表示されることがあります。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OutputOrderReversed ですか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。複数ページのドキュメントが最後のページから最初のページに並べ替えられるかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。</p>
<p>EXTERN_GLOBAL シンボルを <em><strong>Outputorderreversed?</strong>と共に使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ReselectFont</strong></p></td>
<td><p></p>
Unidrv が現在のフォントを再選択する必要がある操作を示す定数の一覧。 は、次のいずれかになります: AFTER_GRXDATA-After CmdSend<em>Xxxx</em>data<a href="raster-data-emission-commands.md" data-raw-source="[raster data emission commands](raster-data-emission-commands.md)">ラスターデータ排出コマンド</a>。
AFTER_XMOVE-任意の x 移動<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">カーソルコマンド</a>の後。
AFTER_FF-CmdFF コマンドの後。</td>
<td><p>(省略可能)。 指定しない場合、Unidrv はフォントを再選択しません。</p></td>
</tr>
<tr class="odd">
<td><p>ReverseBandOrderForEvenPages を <em>し<strong>ますか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。反転バンドが有効かどうかを示します。 この属性は、自動二重機能を搭載したプリンターをサポートするために使用されます。つまり、用紙の両面に印刷することができるプリンターです。</p>
<p>詳細については、この表の後のセクションを参照してください。</p></td>
<td><p>この属性の既定値は<strong>FALSE</strong>です。 この属性を<strong>TRUE</strong>に設定すると、縞模様の順序が有効になります。</p>
<p>この属性は再配置可能なグローバル属性です。ルートレベル (<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">ルートレベルのみの属性</a>を参照) に配置して、プリンター構成に依存していないことを示します。また、依存関係がある場合は、* オプションまたは * ケースコンストラクトと共に表示されることもあります。</p></td>
</tr>
<tr class="even">
<td><p>RotateCoordinate を </em><strong>しますか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。プリンターが、ページの向きに合わせて座標系を回転させるコマンドをサポートするかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。 <strong>TRUE</strong>の場合、向き機能の <em>オプションエントリはプリンターコマンドを指定する必要があります。 <a href="conditional-statements.md" data-raw-source="[&lt;/em&gt;Case](conditional-statements.md)"></em>Case</a>エントリには配置できません。</p></td>
</tr>
<tr class="odd">
<td><p>RotateFont を <em>し<strong>ますか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。プリンターがページの向きに合わせてフォントを自動的に回転させるかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。 <strong>True</strong>の場合、*<strong>RotateCoordinate?</strong>も<strong>true</strong>である必要があります。 \* Case エントリには配置できません。</p></td>
</tr>
<tr class="even">
<td><p>RotateRaster を </em><strong>しますか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。プリンターが自動的にラスターデータをページの向きに合わせて回転させるかどうかを示します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。 <strong>True</strong>の場合、<em><strong>RotateCoordinate?</strong>も<strong>true</strong>である必要があります。 \* Case エントリには配置できません。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TextCaps</strong></p></td>
<td><p>プリンターのテキスト機能を示す定数の一覧。 は、TC_<em>xxx</em>の1つ以上のフラグで構成され、 <strong>GetDeviceCaps</strong>につい Windows SDK てのドキュメントの説明に記載されています。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv ではテキスト機能がサポートされていないと見なされます。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

### <a href="" id="additional-information-about--reversebandorderforevenpages-"></a>\*ReverseBandOrderForEvenPages に関する追加情報

オートデュプレックス機能の副作用は、印刷されたばかりのページの下端が、次のページの上端になるようにプリンターに戻されることです。 最初のページを基準として2番目のページの向きを維持するには、2番目のページのラスターイメージを逆の順序でプリンターに送信する必要があります。 つまり、最初に先頭のスキャン行を送信してプリンターが前面に印刷した場合は、最初にバックサイドのスキャンラインを印刷する必要があります。

**ReverseBandOrderForEvenPages?** が**TRUE**で、両面がオンになって \*いる場合、Unidrv は、偶数ページ (奇数ページの裏面) について、各バンドを逆の順序で列挙します。 OEM レンダリングプラグインでは、プリンターに送信する前に1つのデータバンドのみをキャッシュする必要があります。 各バンド内のスキャン行の順序は逆ではないため、プラグインがそのタスクを処理する必要があり、各スキャン行内のビットの順序を逆にする必要もあります。 これはプラグインにとって追加の作業ですが、このプラグインはラスターデータをキャッシュする必要がなく、すぐにプリンターにデータを送信できるという利点があります。

\***ReverseBandOrderForEvenPages?** 属性が評価されるのは、両面が "長辺を綴じる" に設定されている場合に限られ**ます  。** この属性は、両面が "短辺で反転" に設定されている場合は無視されます。

 

次の表に示すように、\***ReverseBandOrderForEvenPages?** 属性とドライバーでシミュレートされたローテーションの両方の値が、バンドの列挙方法に影響します。 **ReverseBandOrderForEvenPages?** が**true**で、両面が選択されていて、印刷するページが2番目 (または後ろ) である \*場合、 **true**の列方向に指定されているバンド列挙の順序が適用されます。 それ以外の場合は、 **FALSE**である列が適用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ドライバーでシミュレートされたローテーション</th>
<th><strong>TRUE</strong>および偶数ページ</th>
<th><strong>FALSE</strong>または奇数ページ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CCW_ROTATE90</p></td>
<td><p>SW_LTOR</p></td>
<td><p>SW_RTOL</p></td>
</tr>
<tr class="even">
<td><p>CCW_ROTATE270</p></td>
<td><p>SW_RTOL</p></td>
<td><p>SW_LTOR</p></td>
</tr>
<tr class="odd">
<td><p>回転なし</p></td>
<td><p>SW_UP</p></td>
<td><p>SW_DOWN</p></td>
</tr>
</tbody>
</table>

 

凡例: SW\_LTOR = 左から右、SW\_RTOL = 右から左、sw\_UP = Bottom から Top、SW\_DOWN = 上から下

OEM レンダリングプラグインは、\***ReverseBandOrderForEvenPages?** 属性を使用せずに自動二重化をサポートできます。 このプラグインでは、ページ全体のすべてのデータをキャッシュし、一番下のスキャン行からプリンターに送信するだけで済みます。 スキャン行とそのページの他のすべてのスキャンラインは、逆順に送信する必要があります。

OEM レンダリングプラグインは、各スキャンラインを使用してビットの順序を反転し、各バンドがプリンターにデータを送信するときのスキャンラインの順序を逆にする必要がある   に**注意**してください。 この処理が必要になるタイミングを判断するには、インデックス SVI\_PAGENUMBER を使用して[**Iprintoemdriveruni::D rvgetstandardvariable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)を呼び出すことによって、pagenumber 標準変数の値を取得します。 ページ番号が奇数の場合、反転は必要ありません。 数値が偶数で、両面が選択されている場合は、反転が必要です。

 

 

 




