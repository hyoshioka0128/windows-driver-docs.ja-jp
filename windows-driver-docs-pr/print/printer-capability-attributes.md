---
title: プリンター機能属性
description: プリンター機能属性
ms.assetid: 3ee98eee-8f46-4bf0-ac2c-f47f8402fa86
keywords:
- プリンターの機能は、WDK Unidrv を属性します。
- 一般的なプリンター WDK Unidrv、プリンターの機能を属性します。
- 機能の WDK Unidrv 属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eefb56f0fc8d4f93c6b7d370972197e986141c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380532"
---
# <a name="printer-capability-attributes"></a>プリンター機能属性





プリンターの機能の属性は[一般的な印刷属性](general-printing-attributes.md)ページ余白、回転、およびすべての用紙サイズと向きに影響されるテキストの印刷機能としてこのようなプリンターの特性を指定します。

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
<td><p><em><strong>MemoryUsage</strong></p></td>
<td><p></p>
プリンターのメモリに格納されているデータの種類を示す定数のリスト。 1 つ以上を指定できます。フォントのラスター ベクター
<p>データ型が表示されているが、プリンターでサポートされていない、する場合は無視されます。</p></td>
<td><p>任意。 指定しない場合、既定値は (フォント、ラスター、ベクトル) の一覧にします。 詳細については、次を参照してください。<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">プリンター メモリの構成を記述する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>OEMCustomData</strong></p></td>
<td><p>指定する文字列を引用符で囲まれた、<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">プラグインでレンダリング</a>呼び出し時に<a href="https://msdn.microsoft.com/library/windows/hardware/ff553128" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553128)"> <strong>IPrintOemDriverUni::DrvGetGPDData</strong></a>します。</p></td>
<td><p>レンダリングのプラグイン呼び出しの場合に必要な<strong>IPrintOemDriverUni::DrvGetGPDData</strong>します。</p>
<p>テキスト文字列の内容の解釈は、プラグインのレンダリングによって決定されます。</p>
<p>この属性は、再配置可能なグローバル属性。ルート レベルに配置することがあります (を参照してください<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 属性</a>) プリンター構成では、依存関係がないかでが表示されることを示すために<em>オプションまたは * の場合は、いくつかの依存関係がある場合を構築します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OutputOrderReversed でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、最初にマルチページ ドキュメントが最後のページを並べ替えるかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p>
<p>使用していない EXTERN_GLOBAL 記号<em> <strong>OutputOrderReversed?</strong>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ReselectFont</strong></p></td>
<td><p></p>
操作の現在のフォントが Unidrv を再度選択する必要がありますかを示す定数の一覧です。 次になります。すべて CmdSend 後 - AFTER_GRXDATA<em>Xxxx</em>データ<a href="raster-data-emission-commands.md" data-raw-source="[raster data emission commands](raster-data-emission-commands.md)">ラスター データ出力コマンド</a>します。
X 移動後の AFTER_XMOVE<a href="cursor-commands.md" data-raw-source="[cursor commands](cursor-commands.md)">カーソル コマンド</a>します。
AFTER_FF - CmdFF コマンドの後にします。</td>
<td><p>任意。 指定されていない場合は、Unidrv にフォントが再度選択されません。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ReverseBandOrderForEvenPages でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示す反転縞模様が有効になっているかどうか。 この属性は、双方向の自動機能; を持つプリンターをサポートするために使用されます。枚の用紙の両面に印刷できるプリンターは、します。</p>
<p>このテーブルを次のセクションには、詳細が含まれます。</p></td>
<td><p>この属性の既定値は<strong>FALSE</strong>します。 この属性を設定する<strong>TRUE</strong>有効がバンドの順序を反転します。</p>
<p>この属性は、再配置可能なグローバル属性。ルート レベルに配置することがあります (を参照してください<a href="root-level-only-attributes.md" data-raw-source="[Root-Level-Only Attributes](root-level-only-attributes.md)">Root-Level-Only 属性</a>) プリンター構成では、依存関係がないかでが表示されることを示すために * オプションまたは * の場合は、いくつかの依存関係がある場合を構築します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateCoordinate でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、プリンターがページの向きに合わせて座標系を回転するためのコマンドをサポートするかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、<em>オプション エントリ向きの機能は、プリンターのコマンドを指定する必要があります。 配置することはできません、 <a href="conditional-statements.md" data-raw-source="[&lt;/em&gt;Case](conditional-statements.md)"></em>ケース</a>エントリ。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>RotateFont でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、プリンターが自動的にページの向きを一致するようにフォントを回転するかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、し *<strong>RotateCoordinate?</strong>必要もあります<strong>TRUE</strong>します。 配置することはできません、* エントリの場合します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>RotateRaster でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、プリンターが自動的にページの向きに合わせてデータをラスターを回転するかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、し<em> <strong>RotateCoordinate?</strong>必要もあります<strong>TRUE</strong>します。 配置することはできません、* エントリの場合します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>TextCaps</strong></p></td>
<td><p>プリンターのテキストの機能を示す定数のリスト。 1 つ以上の TC_ で構成できます<em>xxx</em>のマイクロソフトの Windows SDK ドキュメントの説明で説明されているフラグ<strong>調べるため</strong>します。</p></td>
<td><p>任意。 指定しない場合、Unidrv では、テキストの機能はサポートされていません前提としています。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

### <a href="" id="additional-information-about--reversebandorderforevenpages-"></a>に関する追加情報\*ReverseBandOrderForEvenPages でしょうか。

自動双方向機能の副作用は、プリンター、次のページの上端になるにだけが印刷されているページの下端をフィードバックすることです。 最初の基準とした 2 つ目のページの向きを維持するには、プリンターに逆の順序で 2 番目のページのラスター イメージを送信します。 つまり、プリンターが前面にあるを出力した最上位のスキャン ラインを最初に送信することによって場合に、する必要があります先に印刷背面の下部にあるスキャン ライン。

ときに\* **ReverseBandOrderForEvenPages?** は**TRUE**と二重化は、Unidrv 各バンド逆の順序での列挙偶数ページ (ページの奇数の裏側)。 プラグインのレンダリング、OEM は、プリンターに送信する前にデータの 1 つだけのバンドをキャッシュする必要があります。 各バンド内でスキャン ラインの順序は反転されませんプラグインする必要があります、そのタスクを引き続き処理し、各スキャン ライン内のビットの順序を逆にする必要がありますもようにします。 プラグイン必要がないこと、ラスター データをキャッシュする利点は、プラグインの余分な作業ですが、プリンターにデータを送信すると、すぐに開始できます。

**注**  、 \* **ReverseBandOrderForEvenPages でしょうか。** 二重化が"長のエッジで反転"に設定されている場合にのみ、属性が評価されます。 「短いエッジで反転」を二重化が設定されている場合、この属性は無視されます。

 

両方の値、 \* **ReverseBandOrderForEvenPages?** 属性と、次の表に示されているドライバー-シミュレートされた回転影響方法バンドが列挙されます。 列で指定された域外列挙の順番の方向で**TRUE**場合に適用されます\* **ReverseBandOrderForEvenPages?** は**TRUE**の二重と選択すると、印刷するページは、2 つ目 (またはバック) にあるとします。 列がそれ以外の場合一番**FALSE**適用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ドライバーのシミュレートされた回転</th>
<th><strong>TRUE</strong>でもページ</th>
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

 

凡例:SW\_LTOR 左から右、SW の =\_RTOL = 右から左、SW\_下から上、SW =\_上から下へのダウン =。

使用せず自動二重化をサポートできるプラグインのレンダリング、OEM、 \* **ReverseBandOrderForEvenPages?** 属性。 プラグインを行うすべてのページ全体のデータのキャッシュ以降、下部にあるスキャン ラインで、プリンターに送信するだけでします。 スキャンする行だけでなく、他のすべてそのページで、逆の順序で送信する必要があります。

**注**  プラグインのレンダリング、OEM がプリンターにデータを送信するために、各スキャン ラインのビットの順序と各バンドでスキャン ラインの順序を反転責任を負います。 ときにこの実行する必要がありますを決定する PageNumber 標準変数の値を取得して、呼び出すことによって[ **IPrintOemDriverUni::DrvGetStandardVariable**](https://msdn.microsoft.com/library/windows/hardware/ff553129)、SVIインデックスを使用して\_PAGENUMBER します。 ページ数が奇数の場合は、逆にすることは必要ありません。 数値が偶数の二重化が選択されている場合は、逆にすることが必要です。

 

 

 




