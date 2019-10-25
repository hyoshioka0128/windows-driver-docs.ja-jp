---
title: ColorMode 機能のオプション属性
description: ColorMode 機能のオプション属性
ms.assetid: e6f68a50-f044-406e-b92c-8449d126bceb
keywords:
- ColorMode 機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a51cbb4075448193fb63342dfc0000df1a39ff43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843056"
---
# <a name="option-attributes-for-the-colormode-feature"></a>ColorMode 機能のオプション属性





次の表に、ColorMode 機能に関連付けられている属性を示します。 ColorMode 機能の詳細については、「[標準機能](standard-features.md)」を参照してください。

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
<td><p>色を <em>し<strong>ますか?</strong></p></td>
<td><p>オプションで色が生成されるかどうかを示す<strong>TRUE</strong>または<strong>FALSE</strong>。</p></td>
<td><p>(省略可能)。 指定しない場合、*<strong>Drvbpp</strong> &gt; 1 の既定値は<strong>TRUE</strong>になります。 グレースケールを作成するには、*<strong>Drvbpp</strong> &gt; 1 を使用して<strong>FALSE</strong>に設定します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Colorplan Eorder</strong></p></td>
<td><p>Unidrv がカラープレーンデータを送信する順序を示す一覧です。</p>
<p>例:</p>
リスト (黄、マゼンタ、シアン、黒) リスト (赤、緑、青)
<p>一覧で色を繰り返すことができます。</p></td>
<td><p><em><strong>DevNumOfPlanes</strong>が1より大きい場合に必要です。 指定された色の数は、*<strong>DevNumOfPlanes</strong>と同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DevBPP</strong></p></td>
<td><p>プリンターでサポートされているカラーデータのピクセルあたりのビット数を示す数値。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は1です。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>DevNumOfPlanes</strong></p></td>
<td><p>プリンターでサポートされているカラープレーンの数を示す数値。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は1です。 (カラープリンターの場合、値1はピクセルモードと呼ばれます)。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DrvBPP</strong></p></td>
<td><p>ビットマップレンダリングバッファーに Unidrv が使用するピクセルあたりのビット数を示す数値。 ビットマップ形式は Windows<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;device-independent bitmap (DIB)&lt;/em&gt;"><em>デバイスに依存しないビットマップ (DIB)</em></a>で、有効な値は1、4、8、16、24、または32です。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は1です。 (カラープリンターの場合、値1は "平面モード" と呼ばれます)。</p>
<p>Windows Dib では、常に1つのカラープレーンを使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ipの <em>id</strong></p></td>
<td><p>表示プラグインの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>Iprintoemuni:: ImageProcessing</strong></a>メソッドに<strong>ipcallbackid</strong>引数として渡される正の数値。</p></td>
<td><p><strong>Iprintoemuni:: ImageProcessing</strong>メソッドを含む<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">レンダリングプラグイン</a>が提供される場合に必要です。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>パレットはプログラミング可能ですか。</strong></p></td>
<td><p>カラーパレットがプログラミング可能かどうかを示す<strong>TRUE</strong>または<strong>FALSE</strong>。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>になります。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>PaletteSize</strong></p></td>
<td><p>指定されたオプションで使用されるカラーパレット内のエントリの数を表す数値。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は2です。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RasterMode</strong></p></td>
<td><p>DIRECT または INDEXED (ラスターデータがプリンターに直接送信されるか、カラーパレットを使用してインデックスが作成されるかを示す)。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値のインデックスが作成されます。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

その他のオプション属性の詳細については、「[すべての機能のオプション属性](option-attributes-for-all-features.md)」を参照してください。

「[画質の制御](controlling-image-quality.md)」も参照してください。

 

 




