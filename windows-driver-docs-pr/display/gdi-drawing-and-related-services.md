---
title: GDI 描画と関連サービス
description: GDI 描画と関連サービス
ms.assetid: b5df84ae-05cf-49dc-aa49-79f912ecd029
keywords:
- サービスの描画、GDI WDK Windows 2000 の表示
- グラフィック ドライバー WDK Windows 2000 を表示するサービスの描画
- 描画の WDK GDI、サポートされているサービスの描画
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99ff67b3900fa6d7f384462fe8c7262f8e9240f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527855"
---
# <a name="gdi-drawing-and-related-services"></a>GDI 描画と関連サービス


## <span id="ddk_gdi_drawing_and_related_services_gg"></span><span id="DDK_GDI_DRAWING_AND_RELATED_SERVICES_GG"></span>


サポートするために、 [ **CLIPOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff539417)、 [ **BRUSHOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff538261)、および[ **XFORMOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570618)構造体、GDI が次の表に、いくつかの描画サービスを提供しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI 描画サービス関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538262" data-raw-source="[&lt;strong&gt;BRUSHOBJ_hGetColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538262)"><strong>BRUSHOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>指定されたブラシの色変換を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538263" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvAllocRbrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538263)"><strong>BRUSHOBJ_pvAllocRbrush</strong></a></p></td>
<td align="left"><p>ドライバーのメモリを割り当てます&#39;ブラシの s 実現します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538264" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvGetRbrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538264)"><strong>BRUSHOBJ_pvGetRbrush</strong></a></p></td>
<td align="left"><p>ドライバーへのポインターを返します&#39;ブラシの s 実現します。 まだ実現されていない場合は、ブラシを認識しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538265" data-raw-source="[&lt;strong&gt;BRUSHOBJ_ulGetBrushColor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538265)"><strong>BRUSHOBJ_ulGetBrushColor</strong></a></p></td>
<td align="left"><p>指定の純色ブラシの RGB 色を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539420" data-raw-source="[&lt;strong&gt;CLIPOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539420)"><strong>CLIPOBJ_bEnum</strong></a></p></td>
<td align="left"><p>クリップ領域から四角形のバッチを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539421" data-raw-source="[&lt;strong&gt;CLIPOBJ_cEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539421)"><strong>CLIPOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>列挙には、すべての四角形またはクリップされる領域の一部のパラメーターを設定します。 (この関数を呼び出すことがなく、リージョンを 1 回列挙できますが、後続の列挙体は、この関数を必要と&#39;件)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539423" data-raw-source="[&lt;strong&gt;CLIPOBJ_ppoGetPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539423)"><strong>CLIPOBJ_ppoGetPath</strong></a></p></td>
<td align="left"><p>パスとしての複雑な領域の取得に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564182" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564182)"><strong>EngAlphaBlend</strong></a></p></td>
<td align="left"><p>ビット ブロック転送機能を提供します<a href="https://msdn.microsoft.com/library/windows/hardware/ff556270#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>アルファ ブレンド</em></a>します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556176" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556176)"> <strong>DrvAlphaBlend</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564185" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564185)"><strong>EngBitBlt</strong></a></p></td>
<td align="left"><p>一般的なビット ブロック転送機能を提供間<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>サーフェスのデバイスで管理された</em></a>、間またはデバイス管理の画面と標準の形式を GDI で管理されたビットマップ。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556180" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556180)"> <strong>DrvBitBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564193" data-raw-source="[&lt;strong&gt;EngControlSprites&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564193)"><strong>EngControlSprites</strong></a></p></td>
<td align="left"><p>破棄します。 または、指定した WNDOBJ 領域でスプライトを再描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564196" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564196)"><strong>EngCopyBits</strong></a></p></td>
<td align="left"><p>デバイスで管理されたラスター サーフェスと GDI 標準形式のビットマップを変換します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"> <strong>DrvCopyBits</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564202" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564202)"><strong>EngCreateClip</strong></a></p></td>
<td align="left"><p>割り当て、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff539417" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539417)"> <strong>CLIPOBJ</strong> </a>ドライバーの&#39;s 一時的に使用します。 ドライバーを呼び出す必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff564786" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564786)"> <strong>EngDeleteClip</strong> </a>不要になったときに削除する関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564786" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564786)"><strong>EngDeleteClip</strong></a></p></td>
<td align="left"><p>割り当てられた CLIPOBJ の削除、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff564202" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564202)"> <strong>EngCreateClip</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564838" data-raw-source="[&lt;strong&gt;EngDeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564838)"><strong>EngDeviceIoControl</strong></a></p></td>
<td align="left"><p>制御コードを指定された操作を実行するデバイスの原因と、指定されたビデオのミニポート ドライバーに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564860" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564860)"><strong>EngFillPath</strong></a></p></td>
<td align="left"><p>(描画) を入力するパスを指定します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556220" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556220)"> <strong>DrvFillPath</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564957" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564957)"><strong>EngGradientFill</strong></a></p></td>
<td align="left"><p>指定したグラフィックス プリミティブ網掛けを適用します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556236" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556236)"> <strong>DrvGradientFill</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564962" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564962)"><strong>EngLineTo</strong></a></p></td>
<td align="left"><p>1 つ、solid、整数のみの表面的な線を描画します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556245" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556245)"> <strong>DrvLineTo</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564977" data-raw-source="[&lt;strong&gt;EngMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564977)"><strong>EngMovePointer</strong></a></p></td>
<td align="left"><p>デバイスでは、エンジンに管理されたポインターを移動します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556248" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556248)"> <strong>DrvMovePointer</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564981" data-raw-source="[&lt;strong&gt;EngPaint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564981)"><strong>EngPaint</strong></a></p></td>
<td align="left"><p>指定した領域を塗りつぶします。 これは、廃止されたの GDI シミュレーション<a href="https://msdn.microsoft.com/library/windows/hardware/ff556256" data-raw-source="[&lt;strong&gt;DrvPaint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556256)"> <strong>DrvPaint</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564982" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564982)"><strong>EngPlgBlt</strong></a></p></td>
<td align="left"><p>回転のビット ブロック転送を実行します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556258" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556258)"> <strong>DrvPlgBlt</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565017" data-raw-source="[&lt;strong&gt;EngSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565017)"><strong>EngSetPointerShape</strong></a></p></td>
<td align="left"><p>ポインターの形状を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565018" data-raw-source="[&lt;strong&gt;EngSetPointerTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565018)"><strong>EngSetPointerTag</strong></a></p></td>
<td align="left"><p>アプリケーションの論理和である図形を作成します。&#39;s ポインターの形で<a href="https://msdn.microsoft.com/library/windows/hardware/ff556289" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556289)"> <strong>DrvSetPointerShape</strong> </a>他の呼び出しでは、ミラー化されたシステムでドライバーが関連付けられています。</p>
<div>
 
</div>
この関数は、Windows 2000 の廃止以降です。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565025" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565025)"><strong>EngStretchBlt</strong></a></p></td>
<td align="left"><p>伸縮ビット ブロック転送を実行します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556302" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556302)"> <strong>DrvStretchBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565027" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565027)"><strong>EngStretchBltROP</strong></a></p></td>
<td align="left"><p>使用して伸縮ビット ブロック転送を実行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff556331#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556306" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556306)"> <strong>DrvStretchBltROP</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565030" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565030)"><strong>EngStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>ストローク (描画) パスを同時に入力するとします。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556311" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556311)"> <strong>DrvStrokeAndFillPath</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565033" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565033)"><strong>EngStrokePath</strong></a></p></td>
<td align="left"><p>ストローク (描画) のパス。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"> <strong>DrvStrokePath</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565037" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565037)"><strong>EngTransparentBlt</strong></a></p></td>
<td align="left"><p>透過的な blt を実行します。 これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557283" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557283)"> <strong>DrvTransparentBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570623" data-raw-source="[&lt;strong&gt;XFORMOBJ_bApplyXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570623)"><strong>XFORMOBJ_bApplyXform</strong></a></p></td>
<td align="left"><p>ポイントの指定した配列に指定された変換またはその逆に適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570627" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetFloatObjXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570627)"><strong>XFORMOBJ_iGetFloatObjXform</strong></a></p></td>
<td align="left"><p>ドライバーに FLOATOBJ 変換ファイルをダウンロードします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570630" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570630)"><strong>XFORMOBJ_iGetXform</strong></a></p></td>
<td align="left"><p>ドライバーには、変換をダウンロードします。</p></td>
</tr>
</tbody>
</table>

 

 

 





