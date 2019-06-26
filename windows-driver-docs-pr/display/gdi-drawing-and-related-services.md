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
ms.openlocfilehash: 15c8f5cfab2b7d971e7fcf70da986c6883cbbba3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379485"
---
# <a name="gdi-drawing-and-related-services"></a>GDI 描画と関連サービス


## <span id="ddk_gdi_drawing_and_related_services_gg"></span><span id="DDK_GDI_DRAWING_AND_RELATED_SERVICES_GG"></span>


サポートするために、 [ **CLIPOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)、 [ **BRUSHOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)、および[ **XFORMOBJ** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570618(v=vs.85))構造体、GDI が次の表に、いくつかの描画サービスを提供しています。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform" data-raw-source="[&lt;strong&gt;BRUSHOBJ_hGetColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform)"><strong>BRUSHOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>指定されたブラシの色変換を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvAllocRbrush&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush)"><strong>BRUSHOBJ_pvAllocRbrush</strong></a></p></td>
<td align="left"><p>ブラシのドライバーの実現のメモリを割り当てます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush" data-raw-source="[&lt;strong&gt;BRUSHOBJ_pvGetRbrush&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush)"><strong>BRUSHOBJ_pvGetRbrush</strong></a></p></td>
<td align="left"><p>ブラシのドライバーの実現にポインターを返します。 まだ実現されていない場合は、ブラシを認識しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor" data-raw-source="[&lt;strong&gt;BRUSHOBJ_ulGetBrushColor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_ulgetbrushcolor)"><strong>BRUSHOBJ_ulGetBrushColor</strong></a></p></td>
<td align="left"><p>指定の純色ブラシの RGB 色を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_benum" data-raw-source="[&lt;strong&gt;CLIPOBJ_bEnum&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_benum)"><strong>CLIPOBJ_bEnum</strong></a></p></td>
<td align="left"><p>クリップ領域から四角形のバッチを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart" data-raw-source="[&lt;strong&gt;CLIPOBJ_cEnumStart&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart)"><strong>CLIPOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>列挙には、すべての四角形またはクリップされる領域の一部のパラメーターを設定します。 (この関数を呼び出すことがなく、リージョンを 1 回列挙できますが、後続の列挙体がこの関数の使用が必要です。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath" data-raw-source="[&lt;strong&gt;CLIPOBJ_ppoGetPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath)"><strong>CLIPOBJ_ppoGetPath</strong></a></p></td>
<td align="left"><p>パスとしての複雑な領域の取得に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
<td align="left"><p>ビット ブロック転送機能を提供します<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>アルファ ブレンド</em></a>します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"> <strong>DrvAlphaBlend</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
<td align="left"><p>一般的なビット ブロック転送機能を提供間<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>サーフェスのデバイスで管理された</em></a>、間またはデバイス管理の画面と標準の形式を GDI で管理されたビットマップ。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)"> <strong>DrvBitBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcontrolsprites" data-raw-source="[&lt;strong&gt;EngControlSprites&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcontrolsprites)"><strong>EngControlSprites</strong></a></p></td>
<td align="left"><p>破棄します。 または、指定した WNDOBJ 領域でスプライトを再描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
<td align="left"><p>デバイスで管理されたラスター サーフェスと GDI 標準形式のビットマップを変換します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"> <strong>DrvCopyBits</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)"><strong>EngCreateClip</strong></a></p></td>
<td align="left"><p>割り当て、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)"> <strong>CLIPOBJ</strong> </a>ドライバーの一時的に使用します。 ドライバーを呼び出す必要があります、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"> <strong>EngDeleteClip</strong> </a>不要になったときに削除する関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip" data-raw-source="[&lt;strong&gt;EngDeleteClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteclip)"><strong>EngDeleteClip</strong></a></p></td>
<td align="left"><p>割り当てられた CLIPOBJ の削除、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip" data-raw-source="[&lt;strong&gt;EngCreateClip&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)"> <strong>EngCreateClip</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol" data-raw-source="[&lt;strong&gt;EngDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)"><strong>EngDeviceIoControl</strong></a></p></td>
<td align="left"><p>制御コードを指定された操作を実行するデバイスの原因と、指定されたビデオのミニポート ドライバーに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
<td align="left"><p>(描画) を入力するパスを指定します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"> <strong>DrvFillPath</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
<td align="left"><p>指定したグラフィックス プリミティブ網掛けを適用します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"> <strong>DrvGradientFill</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
<td align="left"><p>1 つ、solid、整数のみの表面的な線を描画します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"> <strong>DrvLineTo</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer" data-raw-source="[&lt;strong&gt;EngMovePointer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer)"><strong>EngMovePointer</strong></a></p></td>
<td align="left"><p>デバイスでは、エンジンに管理されたポインターを移動します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)"> <strong>DrvMovePointer</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engpaint" data-raw-source="[&lt;strong&gt;EngPaint&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engpaint)"><strong>EngPaint</strong></a></p></td>
<td align="left"><p>指定した領域を塗りつぶします。 これは、廃止されたの GDI シミュレーション<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvpaint" data-raw-source="[&lt;strong&gt;DrvPaint&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvpaint)"> <strong>DrvPaint</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
<td align="left"><p>回転のビット ブロック転送を実行します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)"> <strong>DrvPlgBlt</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape" data-raw-source="[&lt;strong&gt;EngSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape)"><strong>EngSetPointerShape</strong></a></p></td>
<td align="left"><p>ポインターの形状を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointertag" data-raw-source="[&lt;strong&gt;EngSetPointerTag&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointertag)"><strong>EngSetPointerTag</strong></a></p></td>
<td align="left"><p>アプリケーションのポインターの形で論理和を上にある図形を作成します。 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"> <strong>DrvSetPointerShape</strong> </a>他の呼び出しでは、ミラー化されたシステムでドライバーが関連付けられています。</p>
<div>
 
</div>
この関数は、Windows 2000 の廃止以降です。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
<td align="left"><p>伸縮ビット ブロック転送を実行します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"> <strong>DrvStretchBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
<td align="left"><p>使用して伸縮ビット ブロック転送を実行する<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"> <strong>DrvStretchBltROP</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>ストローク (描画) パスを同時に入力するとします。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"> <strong>DrvStrokeAndFillPath</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
<td align="left"><p>ストローク (描画) のパス。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"> <strong>DrvStrokePath</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
<td align="left"><p>透過的な blt を実行します。 これは、GDI シミュレーション、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"> <strong>DrvTransparentBlt</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_bApplyXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_bapplyxform)"><strong>XFORMOBJ_bApplyXform</strong></a></p></td>
<td align="left"><p>ポイントの指定した配列に指定された変換またはその逆に適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetFloatObjXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetfloatobjxform)"><strong>XFORMOBJ_iGetFloatObjXform</strong></a></p></td>
<td align="left"><p>ドライバーに FLOATOBJ 変換ファイルをダウンロードします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform" data-raw-source="[&lt;strong&gt;XFORMOBJ_iGetXform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xformobj_igetxform)"><strong>XFORMOBJ_iGetXform</strong></a></p></td>
<td align="left"><p>ドライバーには、変換をダウンロードします。</p></td>
</tr>
</tbody>
</table>

 

 

 





