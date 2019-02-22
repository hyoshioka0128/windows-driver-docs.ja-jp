---
title: GDI ピクセルあたり 8 ビット CMY マスク モードを使用します。
description: GDI ピクセルあたり 8 ビット CMY マスク モードを使用します。
ms.assetid: 0631f292-c1f1-4627-b116-0b54a34ea295
keywords:
- GDI WDK Windows 2000 の表示、ハーフトーン
- グラフィックス ドライバー WDK Windows 2000 の表示、ハーフトーン
- 描画の WDK GDI、ハーフトーン
- ハーフトーン WDK GDI
- ピクセルあたり 8 ビット CMY マスク モード WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9500b22bbb52cc6530a8f618cc56d6aa53d7d6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552075"
---
# <a name="using-gdi-8-bit-per-pixel-cmy-mask-modes"></a>GDI ピクセルあたり 8 ビット CMY マスク モードを使用します。


## <span id="ddk_using_gdi_8_bit_per_pixel_cmy_mask_modes_gg"></span><span id="DDK_USING_GDI_8_BIT_PER_PIXEL_CMY_MASK_MODES_GG"></span>


Microsoft Windows 2000、 [ **HT\_Get8BPPMaskPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff567320)ピクセルあたり 8 ビット モノクロまたは CMY パレット関数が返されます。 CMY パレットの転置インデックスも返されるように、この関数が変更された Windows XP 以降では、ときに、 *Use8BPPMaskPal*にパラメーターが設定されている**TRUE**します。 格納されている値に依存パレットの型が返される*pPaletteEntry*\[0\]とき**HT\_Get8BPPMaskPalette**が呼び出されます。 場合*pPaletteEntry*\[0\]設定されている 'RGB0' に、反転されたインデックスのパレットが返されます。 場合*pPaletteEntry*\[0\]設定は 0 に通常 CMY パレットが返されます。

この動作の変更の理由**HT\_Get8BPPMaskPalette** Windows GDI Rop、パレット内のインデックスでは、パレットの色ではなくに基づいていますが、これを使用することを想定している、パレットのインデックス 0 は常には黒と白は常に最後のインデックス。 GDI は、パレット エントリをチェックしません。 この変更で**HT\_Get8BPPMaskPalette**により正しい ROP が反転される結果ではなく、出力のようになります。

GDI ROP 動作を修正するには、Windows XP 以降の GDI 形式をサポートして、特別な CMY パレット コンポジション CMY マスク パレット エントリの開始時刻を 255 (白) のインデックスし、インデックスのインデックスを開始位置ではなく (黒) 0 までの作業の 0 (白) と 25 のインデックス操作5 (黒)。 反転 CMY モードでは、先頭と末尾のと同じ黒と白のエントリ数が埋め込まれたパレットで、256 エントリの完全なパレットの中央に CMY マスク色のすべてのエントリも移動します。

**注**   、ディスカッションの用語*CMY モード*以前の実装でサポートされているモードを指す[ **HT\_Get8BPPMaskPalette**](https://msdn.microsoft.com/library/windows/hardware/ff567320). 用語*CMY\_反転モード*Windows XP およびそれ以降の GDI、この関数がビットマスクを反転させますでのみサポートされているモードを指すときにインデックス*pPaletteEntry*\[0\] 'RGB0' に設定されます。

 

次の手順は、すべての Windows XP および Windows GDI ハーフトーン ピクセルあたり 8 ビット CMY マスクのモードを使用するドライバーを後で必要です。 Windows 2000 用のドライバーを開発している場合は、ピクセルあたり 8 ビット モノクロ パレットに、ドライバーの使用を制限する必要があります。

1.  設定、 **flHTFlags**のメンバー、 [ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484) HT 構造\_フラグ\_反転\_8BPP\_ビットマスク\_IDX CMY のいずれかでイメージを表示する GDI ように\_反転モード。

2.  設定*pPaletteEntry*\[0\]への呼び出しの前に次のように**HT\_Get8BPPMaskPalette**:

    ```cpp
    pPaletteEntry[0].peRed   = &#39;R&#39;;
    pPaletteEntry[0].peGreen = &#39;G&#39;;
    pPaletteEntry[0].peBlue  = &#39;B&#39;;
    pPaletteEntry[0].peFlags = &#39;0&#39;;
    ```

    これを行うには、呼び出し元を使用する必要があります、 **HT\_設定\_BITMASKPAL2RGB**マクロ (で定義されている*winddi.h*)。 このマクロの使用例を次に示します。

    ```cpp
    HT_SET_BITMASKPAL2RGB(pPaletteEntry)
    ```

    ここで*pPaletteEntry*への呼び出しで渡された受け取るへのポインター、 **HT\_Get8BPPMaskPalette**関数。 このマクロには、実行が完了すると*pPaletteEntry*\[0\] 'RGB0' 文字列が格納されます。

3.  チェック、 *pPaletteEntry*への呼び出しから返されるパラメーター [ **HT\_Get8BPPMaskPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff567320)を使用して、 **HT\_IS\_BITMASKPALRGB**マクロで定義されている*winddi.h*します。 このマクロの使用例を次に示します。

    ```cpp
    InvCMYSupported = HT_IS_BITMASKPALRGB(pPaletteEntry)
    ```

    この式で*pPaletteEntry*に渡された受け取るへのポインター、 **HT\_Get8BPPMaskPalette**関数。 このマクロを返す場合**TRUE**、GDI し*は*反転 CMY ピクセルあたり 8 ビットのビットマスクのモードをサポートします。 呼び出し元は、インク レベルにパレットのインデックスを変換するのに変換テーブルを使用する必要があります。 参照してください[8 ビットのピクセルあたりのインク レベルをハーフトーン インデックス変換](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)この変換テーブルを生成する関数の例についてはします。

    このマクロを返す場合**FALSE**、GDI の現在のバージョン、*しない*反転 CMY ピクセルあたり 8 ビットのビットマスクのモードをサポートします。 その場合は、GDI では、古い CMY noninverted モードのみがサポートされています。

ピクセルあたり 8 ビット CMY をサポートする GDI バージョン\_反転モードでは、意味、 *CMYMask*に渡されるパラメーター値、 [ **HT\_Get8BPPMaskPalette**](https://msdn.microsoft.com/library/windows/hardware/ff567320)関数が変更されました。 次の表は、変更内容をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CMYMask
<div>
 
</div>
Value</th>
<th align="left">CMY モード インデックス
<div>
 
</div>
(pPaletteEntry [0]! = &#39;RGB0&#39;)</th>
<th align="left">CMY_INVERTED モード インデックス
<div>
 
</div>
(pPaletteEntry [0] = = &#39;RGB0&#39;)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0:ホワイト</p>
<div>
 
</div>
1 ~ 254:淡い灰色 -&gt;濃い灰色
<div>
 
</div>
255:黒</td>
<td align="left"><p>0 - 黒</p>
<div>
 
</div>
1 ~ 254:濃い灰色 -&gt;淡い灰色
<div>
 
</div>
255:ホワイト</td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0:ホワイト</p>
<div>
 
</div>
123 に 1:123 5 倍の 5 倍の 5 つの色
<div>
 
</div>
124 ~ 255:黒</td>
<td align="left"><p>65 に 0。黒</p>
<div>
 
</div>
66 189 には:123 5 x 5 x 5 のさらに 1 つの重複する色します。 127 のインデックス位置にあるエントリは、128 をインデックスにコピーされます。
<div>
 
</div>
190 ~ 255:ホワイト
<div>
 
</div>
<div>
 
</div>
XOR ROP が正しく動作するためには、インデックス 127 と 128 の値が重複しています。</td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>0:ホワイト</p>
<div>
 
</div>
1 に 214:214 6 色 x 6 x 6
<div>
 
</div>
215 ~ 255:黒</td>
<td align="left"><p>0 ~ 20:黒</p>
<div>
 
</div>
234 を 21:214 6 色 x 6 x 6
<div>
 
</div>
235 ~ 255:ホワイト</td>
</tr>
<tr class="even">
<td align="left"><p>3 ~ 255</p></td>
<td align="left"><p>0:ホワイト</p>
<div>
 
</div>
1 ~ 254:CxMxY 色ビットマスク
<div>
 
</div>
255:黒
<div>
 
</div>
<div>
 
</div>
上記の製品で、M、C、および Y シアン、マゼンタ、黄のレベルの数はそれぞれ表します。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>:これらのモードでは、有効な組み合わせ必要ありません、シアン、マゼンタ、または黄色のインク レベル 0 のいずれか。 このような組み合わせでは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"> <strong>HT_Get8BPPMaskPalette</strong> </a>で 0 カウント パレットを返すことによって、エラー状態を示す、 <em>pPaletteEntry</em>パラメーター。</td>
<td align="left"><p>0:黒</p>
<div>
 
</div>
1 ~ 254:先頭に黒と末尾に空白が埋め込まれた CxMxY 色を中央揃え
<div>
 
</div>
CxMxY が奇数の場合は、128 のインデックス位置にあるエントリは 127 のインデックス位置にある 1 つの複製です。
<div>
 
</div>
255:ホワイト
<div>
 
</div>
<div>
 
</div>
上記の製品で、M、C、および Y シアン、マゼンタ、黄のレベルの数はそれぞれ表します。
<div>
 
</div>
<div>
 
</div>
<strong>注: </strong>(C x M x Y) のインデックスは、256 エントリ パレットで中央揃えされます。 つまりと同じ数のパレットおよび padding、ハイ エンド白のエントリの下限を padding 黒のエントリがあります。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>:これらのモードでは、有効な組み合わせ必要ありません、シアン、マゼンタ、または黄色のインク レベル 0 のいずれか。 このような組み合わせでは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"> <strong>HT_Get8BPPMaskPalette</strong> </a>で 0 カウント パレットを返すことによって、エラー状態を示す、 <em>pPaletteEntry</em>パラメーター。</td>
</tr>
</tbody>
</table>

 

-   値の*CMYMask* 0 (グレースケール) の呼び出し元を CMY モードまたは CMY 処理できる\_反転モード。 ただし、GDI Rop が CMY でのみ正しく処理される\_反転モード。

    CMY モード:0 ~ 255 は白から黒のグレースケールのインデックスを作成します。

    CMY\_反転モード。インデックス 0 から 255 までは、黒から白に至るまで、グレーのスケールを表します。

-   有効な値に対して*CMYMask* 255 に 1 から呼び出し元が関数の例に示すようを使用する必要があります[8 ビットのピクセルあたりのインク レベルをハーフトーン インデックス変換](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)インク レベルにインデックスを変換します。

-   有効な値に対して*CMYMask* 1 ~ 255、CMY\_反転モードは、配列の先頭と同じ数の配列の末尾に白のエントリを黒のエントリを含むパレットを埋め込みます。 配列の真中は、その他の色で塗りつぶされます。 これにより、カラー パレットのエントリのすべての 256 が対称的に分散されるため、GDI Rop はインデックス ベースでない色に基づく作業正しくします。 色は対称的に分散するときにインデックス位置にある色*N*インデックス位置にある色の反転は、(256 - *N*)。 色とその逆行列をまとめて印刷する場合、結果は黒です。 つまり、特定の色とその逆の場合は、シアンのインクの 2 つのレベルを追加、最大シアンのインク レベルを 2 つのマゼンタのインク レベル、および 2 つの黄色のインク レベルと同様です。 結果として得られるインク レベルを黒に対応しています。

    たとえば、シアン、マゼンタ、黄色の 3 レベルごとの CMY パレットが 27 (3 x 3 x 3) の合計白と黒の色のインデックス。 27 が数が奇数であり、GDI である必要があります、CMY\_反転モード パレットが埋め込まれている GDI 黒と白のエントリ数が等しくない、中間インデックス (インデックス 13 27 色の) にあるエントリが重複します。 13 および 14 を今すぐにインデックスのエントリで同じ場合パレットは今すぐ 28 の色があります。 パレットを入力するには、GDI パレット (インデックス 0 に 113) の先頭に 114 黒のエントリを配置は 28 色インデックス 114 で (黒) 141 を通じて (白) し、(インデックス 255 までから 142) ホワイト 114 の残りのエントリで塗りつぶします。 これで、256 エントリの合計 (114 + 28 + 114 = 256 エントリ)。 インデックスのレイアウトにより、すべて Rop を正しくレンダリングされます。 関数の例で[8 ビットのピクセルあたりのインク レベルをハーフトーン インデックス変換](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)インク レベルだけでなく、Windows 2000 CMY332 インデックス変換のテーブルを生成する方法を示します。

    次の表では、前の段落で説明した 3 つのパレット x 3 x 3 シアン、マゼンタ、黄色、およびレベルを示します。 28 の色 (27 元パレットの色と 1 つの重複) は、256 色カラー パレットの途中で黒の先頭と末尾に空白パディングにパディングの量が等しいに埋め込まれます。 パレットが対称の場合、つまりいる場合、インデックス位置にある インク レベル*N*インデックス位置にあるものに追加されます (256 - *N*)、黒になります (シアン、マゼンタ、黄色、およびレベル = 2)。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">パレット インデックス (インデックス 3 x 3 x 3)</th>
    <th align="left">シアン Level0 2</th>
    <th align="left">マゼンタ Level0 2</th>
    <th align="left">黄色の Level0 2</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>0 に 113</p>
    <div>
     
    </div>
黒</td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>114 (0)</p>
    <p>黒</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>115 (1)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>116 (2)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>117 (3)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>118 (4)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>119 (5)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>120 (6)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>121 (7)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>122 (8)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>123 (9)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>124 (10)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>125 (11)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>126 (12)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>127 (13)</p>
    <p>128 のインデックスにコピー</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>128 (14)</p>
    <p>127 をインデックスにあるエントリの重複しています</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>129 (15)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>130 (16)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>131 (17)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>132 (18)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>133 (19)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>134 (20)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>135 (21)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>136 (22)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>137 (23)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>138 (24)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>139 (25)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>140 (26)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>141 (27)</p>
    <p>ホワイト</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>142 ~ 255</p>
    <p>ホワイト</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   要求されたパレットが CMY モード パレットの場合 (CMY いない\_反転モード パレット)、次の値に*CMYMask* 255 3 からは、レンダリングされたピクセルあたり 8 ビット バイトのインデックスのビットは次の意味を持ちます。 します。 この場合は、ビット パターンは、変換なしで直接使用できる インク レベルを表します。 これは、CMY ときにも当てはまります\_反転モード バイトのインデックスは、変換テーブルを使用して CMY モードにマップされて**CMY332Idx**メンバー。 参照してください[8 ビットのピクセルあたりのインク レベルをハーフトーン インデックス変換](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)詳細についてはします。

```cpp
  Bit     7 6 5 4 3 2 1 0
          |   | |   | | |
          +---+ +---+ +-+
            |     |    |
            |     |    +-- Yellow 0-3 (Max. 4 levels)
            |     |
            |     +-- Magenta 0-7 (Max. 8 levels)
            |
            +-- Cyan 0-7 (Max. 8 levels)
```

 

 





