---
title: GDI データ型
description: GDI データ型
ms.assetid: 2054aa16-6d86-4db3-8b16-4570b0374e23
keywords:
- GDI WDK Windows 2000 の表示、データ型
- グラフィックス ドライバー WDK Windows 2000 の表示、データ型
- 描画 WDK GDI やデータ型
- データ型の WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4fa605d9bbd5974a142e4175ff4454e1007a78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385028"
---
# <a name="gdi-data-types"></a>GDI データ型


## <span id="ddk_gdi_data_types_gg"></span><span id="DDK_GDI_DATA_TYPES_GG"></span>


次の表で定義されているデータ型は、デバイス ドライバー インターフェイスに表示されます。 表示されているデータ型のいくつか記載されている既に[ユーザーの GDI オブジェクト](gdi-user-objects.md)します。 ポインターであるデータ型は、アスタリスクでマークされます (\*)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">グラフィックス DDI データ型</th>
<th align="left">変数名のプレフィックス</th>
<th align="left">定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BOOL</p></td>
<td align="left"><p>b</p></td>
<td align="left"><p>いずれかを指定する 32 ビット値<strong>TRUE</strong>または<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BYTE</p></td>
<td align="left"><p>j</p></td>
<td align="left"><p>8 ビット符号なし整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRUSHOBJ<em></p></td>
<td align="left"><p>pbo</p></td>
<td align="left"><p>ブラシ オブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLIPLINE</p></td>
<td align="left"><p>cl</p></td>
<td align="left"><p>Clipline オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLIPOBJ</em></p></td>
<td align="left"><p>pco</p></td>
<td align="left"><p>クリッピング オブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DHPDEV</p></td>
<td align="left"><p>dhpdev</p></td>
<td align="left"><p>物理デバイスを識別するデバイス ドライバーで定義されている 32 ビット ハンドル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DHSURF</p></td>
<td align="left"><p>dhsurf</p></td>
<td align="left"><p>デバイス管理の画面を識別するデバイス ドライバーで定義されている 32 ビット ハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><p>修正プログラム</p></td>
<td align="left"><p>修正プログラム</p></td>
<td align="left"><p>固定小数点数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLOATL</p></td>
<td align="left"><p>E</p></td>
<td align="left"><p>浮動小数点数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOAT_LONG</p></td>
<td align="left"><p>el</p></td>
<td align="left"><p>コンテキストに応じて、時間の長いまたは FLOATL のいずれかとして解釈される 32 ビットのオーバー ロードされた値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLONG</p></td>
<td align="left"><p>fl</p></td>
<td align="left"><p>32 ビット フラグのセット。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FONTOBJ<em></p></td>
<td align="left"><p>pfo</p></td>
<td align="left"><p>フォント オブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSHORT</p></td>
<td align="left"><p>fs</p></td>
<td align="left"><p>16 ビット フラグのセット。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FWORD</p></td>
<td align="left"><p>fw</p></td>
<td align="left"><p>16 ビット符号付き整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBM</p></td>
<td align="left"><p>hbm</p></td>
<td align="left"><p>ビットマップを識別するには、GDI によって定義されている 32 ビット ハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HPAL</p></td>
<td align="left"><p>hpal</p></td>
<td align="left"><p>パレットを識別するには、GDI によって定義されている 32 ビット ハンドル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSURF</p></td>
<td align="left"><p>hsurf</p></td>
<td align="left"><p>サーフェスを識別するには、GDI によって定義されている 32 ビット ハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LONG</p></td>
<td align="left"><p>l</p></td>
<td align="left"><p>32 ビット符号付き整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミックス</p></td>
<td align="left"><p>ミックス</p></td>
<td align="left"><p>下位 16 ビット前景色と背景の混在モードを定義する 32 ビット値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PALOBJ</em></p></td>
<td align="left"><p>ppalo</p></td>
<td align="left"><p>パレット オブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PATHOBJ<em></p></td>
<td align="left"><p>ppo</p></td>
<td align="left"><p>パス オブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTE</p></td>
<td align="left"><p>pte</p></td>
<td align="left"><p>Point 構造体で構成される {FLOATL <strong>x</strong>、 <strong>y</strong>;}。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>POINTFIX</p></td>
<td align="left"><p>ptfx</p></td>
<td align="left"><p>Point 構造体で構成される {修正<strong>x</strong>、 <strong>y</strong>;}。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTQF</p></td>
<td align="left"><p>ptq</p></td>
<td align="left"><p>Point 構造体で構成される {LARGE_INTEGER <strong>x</strong>、 <strong>y</strong>;}。 この構造体の各メンバーは、28.36 形式での 64 ビットの座標です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PWSZ</p></td>
<td align="left"><p>pwsz</p></td>
<td align="left"><p>Null で終わる Unicode 文字列へのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PVOID</p></td>
<td align="left"><p>pv</p></td>
<td align="left"><p>VOID、未定義の型へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECTFX</p></td>
<td align="left"><p>rcfx</p></td>
<td align="left"><p>四角形の構造で構成される {修正<strong>xLeft</strong>、 <strong>yTop</strong>、 <strong>xRight</strong>、 <strong>yBottom</strong>;}。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROP4</p></td>
<td align="left"><p>rop4</p></td>
<td align="left"><p>ソース、宛先、パターン、およびマスク ピクセルを混在させることの方法を指定する 32 ビット値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>短い</p></td>
<td align="left"><p>s</p></td>
<td align="left"><p>16 ビット符号付き整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>サイズ</p></td>
<td align="left"><p>sizl</p></td>
<td align="left"><p>構成される構造 {長い<strong>cx</strong>、 <strong>cy</strong>;}。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STROBJ</em></p></td>
<td align="left"><p>pstro</p></td>
<td align="left"><p>テキストの文字列オブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SURFOBJ<em></p></td>
<td align="left"><p>pso</p></td>
<td align="left"><p>画面のオブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ULONG</p></td>
<td align="left"><p>ul</p></td>
<td align="left"><p>32 ビット符号なし整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT</p></td>
<td align="left"><p>us</p></td>
<td align="left"><p>16 ビット符号なし整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XFORMOBJ</em></p></td>
<td align="left"><p>pxo</p></td>
<td align="left"><p>座標変換オブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XLATEOBJ*</p></td>
<td align="left"><p>pxlo</p></td>
<td align="left"><p>色変換オブジェクトへのポインター。</p></td>
</tr>
</tbody>
</table>

 

使用状況に従って変数名のプレフィックスを変更する、次の表に示すパラメーター プレフィックスが使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プレフィックス</th>
<th align="left">パラメーターの使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>アイコン</p></td>
<td align="left"><p>列挙型のインデックス</p></td>
</tr>
<tr class="even">
<td align="left"><p>c</p></td>
<td align="left"><p>カウント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>ポインター</p></td>
</tr>
</tbody>
</table>

 

 

 





