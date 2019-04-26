---
title: ColorMode 機能のオプション属性
description: ColorMode 機能のオプション属性
ms.assetid: e6f68a50-f044-406e-b92c-8449d126bceb
keywords:
- 返さ機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f635661505a0a8249b061feebf124e41fc0e8e58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339871"
---
# <a name="option-attributes-for-the-colormode-feature"></a>ColorMode 機能のオプション属性





次の表は、返さ機能に関連付けられている属性を一覧表示します。 返さ機能の詳細については、次を参照してください。[標準機能](standard-features.md)します。

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
<td><p><em><strong>色。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、オプションで色を生成するかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>TRUE</strong>の *<strong>DrvBPP</strong> &gt; 1。 灰色のスケーリングを作成するに設定<strong>FALSE</strong>で *<strong>DrvBPP</strong> &gt; 1。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ColorPlaneOrder</strong></p></td>
<td><p>Unidrv がカラー プレーン データを送信する必要がありますの順序を示す一覧です。</p>
<p>例:</p>
一覧 (黄色、マゼンタ、シアン、黒) 一覧 (赤、緑、青)
<p>色の一覧で繰り返すことができます。</p></td>
<td><p>場合に、必ず<em> <strong>DevNumOfPlanes</strong>が 1 より大きい。 指定された色の数と同じにする必要があります *<strong>DevNumOfPlanes</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DevBPP</strong></p></td>
<td><p>プリンターでサポートされている色データの 1 ピクセルあたりのビット数を表す数値を指定します。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>DevNumOfPlanes</strong></p></td>
<td><p>プリンターでサポートされているカラー プレーンの数を示す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。 (カラー プリンターの値を 1 と呼びますピクセル モード。)</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>DrvBPP</strong></p></td>
<td><p>1 ピクセルのビットマップ レンダリング バッファー Unidrv が使用するビット数を示す数値。 ビットマップ形式は、Windows <a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;device-independent bitmap (DIB)&lt;/em&gt;"><em>デバイスに依存しないビットマップ (DIB)</em></a>、有効な値は 1、4、8、16、24、または 32 とします。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。 (カラー プリンターの値を 1 と呼びます「平面モード」。)</p>
<p>Windows Dib では、1 つのカラー プレーン常に使用します。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>IPCallbackID</strong></p></td>
<td><p>正の数値があり、レンダリング プラグインでは、に渡される<a href="https://msdn.microsoft.com/library/windows/hardware/ff554261" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554261)"> <strong>IPrintOemUni::ImageProcessing</strong> </a>メソッドとしてその<strong>IPCallbackID</strong>引数。</p></td>
<td><p>必要な場合、<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-in](rendering-plug-ins.md)">プラグインでレンダリング</a>が指定されてを格納している、 <strong>IPrintOemUni::ImageProcessing</strong>メソッド。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>PaletteProgrammable でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、カラー パレットがプログラミング可能なかどうか。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>PaletteSize</strong></p></td>
<td><p>指定されたオプションと共に使用するカラー パレット内のエントリの数を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 2 です。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>RasterMode</strong></p></td>
<td><p>直接またはインデックス付きかを示すラスター データが、プリンターに直接送信されるかどうかまたはカラー パレット インデックスが作成されます。</p></td>
<td><p>任意。 指定しない場合、既定値は、インデックスを作成します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

追加のオプションの属性については、次を参照してください。[すべての機能のオプション属性](option-attributes-for-all-features.md)します。

参照してください[画質を制御する](controlling-image-quality.md)します。

 

 




