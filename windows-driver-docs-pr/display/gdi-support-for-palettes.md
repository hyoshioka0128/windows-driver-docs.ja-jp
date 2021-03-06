---
title: パレットの GDI サポート
description: パレットの GDI サポート
ms.assetid: 8c6ebf1e-6c83-45d9-bf83-f0684d28fc32
keywords:
- DrvEnablePDEV
- 色、GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、色
- WDK GDI の色の管理
- Windows 2000 の WDK のパレットを表示します。
- WDK の GDI や色の描画
- DrvSetPalette
- WDK GDI の色のインデックス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e700bcc35b583dfc7d0dfda679a225c74395c98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358653"
---
# <a name="gdi-support-for-palettes"></a>パレットの GDI サポート


## <span id="ddk_gdi_support_for_palettes_gg"></span><span id="DDK_GDI_SUPPORT_FOR_PALETTES_GG"></span>


GDI は、パレットの管理に関する作業の大部分を実行できます。 GDI を呼び出すと、 [ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数の場合、ドライバー返しますその既定のパレットに GDI の一部として、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。 このパレットを使用してドライバーを作成する必要があります、 [ **EngCreatePalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)関数。

パレットは、32 ビットを効果的にマップ*カラー インデックス*24 ビットの RGB カラー値には GDI パレットを使用する方法。 GDI は、インデックスが、デバイスに表示するにはさまざまな色を判断できるように、ドライバーは、パレットを指定します。

使用している限り、ドライバーはほとんどのパレット操作および計算処理しない必要があります、 [ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj) GDI によって提供されます。

関数を実装する必要があります、デバイスは、変更可能なパレットをサポートする場合[ **DrvSetPalette**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)します。 GDI 呼び出し*DrvSetPalette*アプリケーションがデバイスのパレットを変更し、結果として得られる新しいパレットをドライバーに渡します。 ドライバーは、新しいパレットをできるだけ一致するように、内部ハードウェア パレットを設定する必要があります。

次の表に示す 2 つの異なる形式のいずれかで GDI のパレットを定義できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パレット形式</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>インデックスを作成</p></td>
<td align="left"><p>色のインデックスは、RGB 値の配列にインデックスです。 大規模で含む、たとえば、4096 色以上のインデックスまたは配列を小規模で、たとえば、16 色は、インデックスを含むことができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビット フィールド</p></td>
<td align="left"><p>色のインデックスのビット フィールドは、それぞれの色で R、G、および B の量の観点から色を指定します。 たとえば、5 ビットされる可能性がありますごとに、各色の 0 から 31 までの値を提供します。 5 ビット値は、RGB に変換するときに、各コンポーネントについては、0 ~ 255 の範囲をカバーするスケール アップです。 (通常の RGB 表現自体は、ビット フィールドによって定義されます)。</p></td>
</tr>
</tbody>
</table>

 

GDI は通常、逆の順序で、パレットのマッピングを使用します。 つまり、アプリケーションで描画の RGB 色を指定して、GDI のデバイスがその色を表示する色のインデックスを見つける必要があります。 次の表に示されるように、GDI、パレットのプライマリ サービスの 2 つの関数を作成して、いくつかのサービス機能と同様に、パレットの削除に関連する、 [ **PALOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_palobj) 、 [**XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)間、2 つのパレット カラー インデックスに変換するために使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette" data-raw-source="[&lt;strong&gt;EngCreatePalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)"><strong>EngCreatePalette</strong></a></p></td>
<td align="left"><p>パレットを作成します。 ドライバーでは、デバイスをパレットを関連付けますのパレットを識別するハンドルを返すことによって、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo" data-raw-source="[&lt;strong&gt;DEVINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)"> <strong>DEVINFO</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepalette" data-raw-source="[&lt;strong&gt;EngDeletePalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepalette)"><strong>EngDeletePalette</strong></a></p></td>
<td align="left"><p>特定のパレットを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdithercolor" data-raw-source="[&lt;strong&gt;EngDitherColor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdithercolor)"><strong>EngDitherColor</strong></a></p></td>
<td align="left"><p>指定された RGB 色を近似する標準 8 x 8 ディザーを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerypalette" data-raw-source="[&lt;strong&gt;EngQueryPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerypalette)"><strong>EngQueryPalette</strong></a></p></td>
<td align="left"><p>その属性のパレットを照会します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors" data-raw-source="[&lt;strong&gt;PALOBJ_cGetColors&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors)"><strong>PALOBJ_cGetColors</strong></a></p></td>
<td align="left"><p>インデックス付きのパレットから RGB 色をダウンロードするためのドライバーを使用します。 ディスプレイ ドライバーによって呼び出される、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)"> <strong>DrvSetPalette</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_cgetpalette" data-raw-source="[&lt;strong&gt;XLATEOBJ_cGetPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_cgetpalette)"><strong>XLATEOBJ_cGetPalette</strong></a></p></td>
<td align="left"><p>24 ビットの RGB 色または、インデックス付きソース パレットの色のビット フィールドの形式を取得します。 ドライバーは、この関数を使用して、色の描画を実行するパレットから情報を取得できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform" data-raw-source="[&lt;strong&gt;XLATEOBJ_hGetColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform)"><strong>XLATEOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>指定した平行移動オブジェクトの色変換を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_ixlate" data-raw-source="[&lt;strong&gt;XLATEOBJ_iXlate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_ixlate)"><strong>XLATEOBJ_iXlate</strong></a></p></td>
<td align="left"><p>変換先の色のインデックスを 1 つのソース カラー インデックスに変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_pivector" data-raw-source="[&lt;strong&gt;XLATEOBJ_piVector&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_pivector)"><strong>XLATEOBJ_piVector</strong></a></p></td>
<td align="left"><p>インデックス付きソース パレットから平行移動ベクターを取得します。 ドライバーは、このベクターを使用して、ソースのインデックスを変換先のインデックスの独自の翻訳を実行します。</p></td>
</tr>
</tbody>
</table>

 

 

 





