---
title: コスメティック線
description: コスメティック線
ms.assetid: eb9651dd-cc77-469f-8441-4bb958bd374d
keywords:
- 線 WDK GDI、外観
- GDI WDK Windows 2000 の表示、線、外観
- グラフィック ドライバー WDK Windows 2000 の表示、線、表面的です
- 描画 WDK GDI、線、外観
- 表面的な行 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dfe54234eba20470d04b46666640ca82c7d19fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390031"
---
# <a name="cosmetic-lines"></a>コスメティック線


## <span id="ddk_cosmetic_lines_gg"></span><span id="DDK_COSMETIC_LINES_GG"></span>


A*表面的な*行が 1 ピクセル幅では常に、単色ブラシを使用して描画します。 これは、表面的な行を表示するためにどのピクセルをオンにするかを決定するグリッドの交点量子化 (GIQ) 用のひし形の規則に従ってレンダリングされます。

次の図は、ピクセルのグリッドの交点にある、四角形グリッドの行を示します。 ピクセルを点灯する必要がありますを確認するのには、ひし形など、線の中央に配置して、沿いにスライド式を想像してください。 ダイヤモンドの幅と高さは、隣接するピクセルのセンターの間の距離に正確に一致します。 線に沿って移動するとき、ひし形、中心がひし形で完全にカバーする任意のピクセルはオンです。 行ポイントを通過中間隣接する 2 つのピクセルの間で場合、ピクセルを有効にするのには、行と隣接するピクセルの指向の方法の傾きに依存: 水平方向に (サイド バイ サイド)、または垂直方向に (他の上に 1 つ)。

次の表では、このような場合を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">(絶対値) の線の傾き</th>
<th align="left">隣接するピクセル</th>
<th align="left">結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>傾き&lt;1</p>
<div>
 
</div>
または
<div>
 
</div>
傾き&gt;1</td>
<td align="left"><p>水平方向に</p></td>
<td align="left"><p>ライトのひし形の左側の頂点でピクセルです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>傾き&lt;1</p>
<div>
 
</div>
または
<div>
 
</div>
傾き&gt;1</td>
<td align="left"><p>垂直方向に</p></td>
<td align="left"><p>ダイヤモンドの最上位の頂点でピクセルを点灯します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>傾き = 1</p></td>
<td align="left"><p>水平方向に</p></td>
<td align="left"><p>ダイヤモンドの最上位の頂点でピクセルを点灯します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>傾き = 1</p></td>
<td align="left"><p>垂直方向に</p></td>
<td align="left"><p>ひし形の適切な頂点でピクセルを点灯します。</p></td>
</tr>
</tbody>
</table>

 

行を各列に 1 ピクセルが-1 と 1、行の行ごとに 1 ピクセルと勾配の絶対値では 1 より大きいと傾斜ダイヤモンド規則のライトです。 これにより、ギャップを表面的な行が表示されます。

表面的な行の先頭と末尾のピクセルは、ダイヤモンド規則によっても決まります。 表面的な行が最初のピクセル包括および最後のピクセルの排他;つまり、ピクセルのダイヤモンド内で直線の開始、そのピクセルが点灯します。 同様に、行は、ピクセルのダイヤモンド内で終了した場合、そのピクセルは点灯しません。

次のグラフは、表面的な行のダイヤモンドの規則を示しています。

![表面的な行のダイヤモンドの規則を示す図](images/102-01b.png)

表面的な行を表示するため、 [ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)関数が GIQ ひし形の規則に従います。 [ **DrvLineTo** ](https://msdn.microsoft.com/library/windows/hardware/ff556245)関数は、Microsoft Win32 にアプリケーション呼び出しの最適化としてドライバーを提供できる省略可能なエントリ ポイント**LineTo**関数。 **DrvLineTo**よりも簡単です**DrvStrokePath**整数エンドポイントと表面的な実線のみをサポートしているためです。

R2 をサポートするラスター デバイス\_混合モードでは、その逆に、コピー先の色を変更するバイナリのラスター オペレーション、ドライバーは、正確なレンダリングを使用する必要があります。 レンダリングは、GDI とドライバーの両方でレンダリングを必要とするデバイスの正確な必要があります。 GDI は一部のビットマップを描画します。 デバイスが含まれ、ドライバーは、(、ピクセルが小さすぎて表示違いがある) 場合を除き、他の面で描画します。 これには、複雑なクリッピングを処理する GDI を要求するデバイスも含まれています。

 

 





