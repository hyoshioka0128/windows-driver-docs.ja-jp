---
title: 破棄とフック
description: 破棄とフック
ms.assetid: 52544915-8392-4eb1-8186-6a7fbad8ed4a
keywords:
- セキュリティ ネゴシエーション WDK GDI、フック
- ネゴシエーション punting の WDK GDI を画面します。
- WDK GDI のフック
- WDK GDI punting
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdec2fc10f763a97677a46b65f684a7ded760a85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380222"
---
# <a name="hooking-versus-punting"></a>破棄とフック


## <span id="ddk_hooking_versus_punting_gg"></span><span id="DDK_HOOKING_VERSUS_PUNTING_GG"></span>


条件*フック*と*punting*提供する描画操作では、標準のビットマップを提供または GDI 依存かどうか、ドライバーの意思決定を参照してください。 ドライバーは、サーフェスのエンジン管理を実装する場合、GDI は、すべての描画操作を処理できます。 1 つまたは複数のドライバー、ただし、提供、[描画関数](optional-display-driver-functions.md)場合は、ハードウェアには、これらの操作が高速化できます。 これは、実装、または、フックして、 *DrvXxx*関数。

ドライバー開発者は、特定のグラフィックス DDI エントリ ポイントを実装する描画操作のサブセットのみを実装する必要があります。 すべての操作は、ドライバーがサポートしていない、それらを実行するために、適切な GDI 関数を呼び出すことができます。これは gdi punting としてと呼ばれます。 これは、状況によっては、ドライバーに、操作を実装する必要があります。 たとえば、ドライバーは、デバイス管理の画面を実装する場合、ディスプレイ ドライバーで特定の描画機能を実装しなければなりません。

### <a name="span-idhookingspanspan-idhookingspanspan-idhookingspanhooking"></a><span id="Hooking"></span><span id="hooking"></span><span id="HOOKING"></span>フックします。

既定では、描画サーフェイスはエンジン管理の画面では、ときに、GDI は描画 (表示) 操作を処理します。 アクセラレータの一部またはすべての特定の画面の描画機能を提供するハードウェアを活用したり、ドライバーのブロックを特別な転送のハードウェアを使用して、これらの関数をフックできます。 呼び出しをフックするドライバーを指定します、フックとしてのフラグ、 *flHook*のパラメーター、 [ **EngAssociateSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)と[ **EngModifySurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface)関数。

ドライバーは、関数のフック フラグを指定する場合は、サポートされているグラフィック DDI エントリ ポイントの一覧でその関数を提供します。 ドライバーは、操作を最適化できますが、ハードウェアのサポート。 このようなドライバーは、かぎ状の呼び出しで特定のケースのみを処理できます。 たとえば、複雑なグラフィックスは、接続されている呼び出しで要求された場合、可能性がありますコールバックを後回しに GDI や GDI、操作を処理できるようにする方が効率的。

かぎ状の呼び出しを処理するかどうかを選択したドライバーの別の例を次に示します。 特定のビット ブロック転送呼び出しを処理できるハードウェアをサポートしているドライバーを検討してください。 *Rop*します。 場合でも、このドライバーは、独自の多くの操作を行うことができます、フレーム バッファーだけで、それ以外の場合。 このようなドライバーは、フレーム バッファーのビットマップの画面にハンドルのサーフェイスとして返すはその*PDEV*がフックされますが、 [ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)自体を呼び出します。 GDI を呼び出すと*DrvBitBlt*ドライバーは、ハードウェアでサポートされているいずれかがその ROP を確認できます。 そうでないドライバーはへの呼び出しで GDI に戻す操作を渡すことができる場合、 [ **EngBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)関数。

サーフェスのデバイス管理をサポートするドライバーをいくつかの描画の関数では; をフックする必要があります。namely [ **DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)、 [ **DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)、および[ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath). GDI のシミュレーションでは、その他の描画機能を処理できますが、お勧めこの型用のフックのドライバーがなど、他の関数を out パフォーマンスの理由により、 [ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)と[**DrvRealizeBrush** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)シミュレーションし、画面に描画を必要とするために機能します。

### <a name="span-idpuntingspanspan-idpuntingspanspan-idpuntingspanpunting"></a><span id="Punting"></span><span id="punting"></span><span id="PUNTING"></span>Punting

*Punting* GDI へのコールバックに対応する GDI シミュレーションへの呼び出しを配置することを意味します。 一般に、すべて*DrvXxx*グラフィックの呼び出しが対応する GDI **への Eng * * * Xxx*同じ引数を受け取る呼び出しをシミュレーションします。 ドライバーには、ビットマップ nonopaque が行われて、限り GDI シミュレーションに変更なしのすべてのパラメーターを渡されることができます。 ドライバーは、GDI に punts 呼び出しごとに、(その機能のコードを省略できます) ので、ドライバーのサイズが減少します。 ただし、エンジンに、呼び出しが所有しているため、ドライバーは、実行速度を制御がありません。 いくつかの複雑な場合、ある可能性がありますいないドライバーのサポートを提供する実際的なメリットです。

### <a name="span-idhookable_gdi_graphics_output_functionsspanspan-idhookable_gdi_graphics_output_functionsspanspan-idhookable_gdi_graphics_output_functionsspanhookable-gdi-graphics-output-functions"></a><span id="Hookable_GDI_Graphics_Output_Functions"></span><span id="hookable_gdi_graphics_output_functions"></span><span id="HOOKABLE_GDI_GRAPHICS_OUTPUT_FUNCTIONS"></span>フックの GDI グラフィックス出力関数

グラフィックは、ドライバーが接続できるし、対応する GDI シミュレーションは、次の表に記載されている関数を出力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのグラフィックス出力関数</th>
<th align="left">対応する GDI シミュレーション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtextout" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtextout)"><strong>EngTextOut</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





