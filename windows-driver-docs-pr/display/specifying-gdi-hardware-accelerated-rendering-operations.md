---
title: GDI ハードウェア高速化レンダリング操作の指定
description: GDI ハードウェア高速化レンダリング操作の指定
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- GDI ハードウェア アクセラレータを WDK を表示して操作を表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10600a7813112b2a9e63c23fcd23942e86acec8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356349"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>GDI ハードウェア高速化レンダリング操作の指定


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


ときに、 [ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数が呼び出されると、オペレーティング システムを使用して実行する GDI ハードウェア アクセラレータによるレンダリング操作の種類を指定します、 *pRenderKmArgs*パラメーター。 DirectX グラフィックスのカーネル サブシステムのディスプレイ ポート ドライバー (*Dxgkrnl.sys*) 設定、 *pRenderKmArgs*-&gt;**pCommand**メンバー可変サイズの配列が含まれたコマンド バッファーを指す[ **DXGK\_RENDERKM\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)構造体。 また、設定、 *pRenderKmArgs*-&gt;**pCommandLength**メンバー (バイト単位) をコマンド バッファーのサイズにします。

ドライバーは、入力 DXGK を変換する必要があります\_RENDERKM\_コマンドのコマンドは、DMA バッファー コマンドにバッファーし、修正プログラムの場所の一覧を作成します。

DXGK\_RENDERKM\_の次の表に示すコマンドには、GDI ハードウェア アクセラレータによるレンダリング操作の特性を指定するメンバーが含まれます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表示操作</th>
<th align="left">DXGK_RENDERKM_COMMAND メンバー</th>
<th align="left">対応する DXGK_GDIARG_XXX 構造</th>
<th align="left">対応する DXGK_RENDERKM_OPERATION 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>アルファ ブレンド</p></td>
<td align="left"><p>AlphaBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>伸縮しないでビット ブロック転送</p></td>
<td align="left"><p>Bitblt 関数</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType とアンチ エイリアス化テキスト ピクセル blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>色の塗りつぶし</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビット ブロック転送を拡大</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>透過性のビット ブロック転送</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

オペレーティング システムの使用、**オペコード**DXGK のメンバー\_RENDERKM\_ディスプレイのミニポート ドライバーを処理する必要がある特定の GDI ハードウェア アクセラレータによるレンダリング操作を示すコマンド。 **オペコード**型のメンバーは、 [ **DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)表に示した値を使用します。

オペレーティング システムが、DXGK の適切な値を指定することも\_RENDERKM\_コマンド**CommandSize**メンバーで、バイト単位の値を含む、現在のレンダリング コマンドのサイズを指定します。**オペコード**とコマンドのサブ四角形の数。

透過性でビット ブロック転送を実行するディスプレイ アダプターの機能に関する情報を提供するさらに、 [ **D3DKM\_TRANSPARENTBLTFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)に含まれている構造体DXGK\_GDIARG\_TRANSPARENTBLT -&gt;**フラグ**メンバー。

 

 





