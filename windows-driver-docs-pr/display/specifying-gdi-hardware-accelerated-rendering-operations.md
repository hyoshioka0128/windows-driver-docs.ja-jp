---
title: GDI ハードウェア高速化レンダリング操作の指定
description: GDI ハードウェア高速化レンダリング操作の指定
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- GDI ハードウェアアクセラレーションの WDK ディスプレイを使用したレンダリング操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f92d668be6bd642b8d87d3dc21c4620c27fbcf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825726"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>GDI ハードウェア高速化レンダリング操作の指定


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数が呼び出されると、オペレーティングシステムは、 *Prenderkmargs*パラメーターを介して実行する GDI ハードウェアアクセラレータレンダリング操作の種類を指定します。 DirectX グラフィックスカーネルサブシステム (*Dxgkrnl*) のディスプレイポートドライバーは、DXGK の変数サイズの配列を含むコマンドバッファーを指すように*Prenderkmargs*-&gt;**pcommand**メンバーを設定[ **\_RENDERKM\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)の構造体。 また、 *Prenderkmargs*-&gt;**pcommandlength**メンバーをコマンドバッファーのサイズ (バイト単位) に設定します。

ドライバーは、入力 DXGK\_RENDERKM\_コマンドコマンドバッファーを DMA バッファーコマンドに変換し、修正プログラムの場所の一覧を作成する必要があります。

DXGK\_RENDERKM\_コマンドには、次の表に示すように、GDI ハードウェアアクセラレータのレンダリング操作の特性を指定するメンバーが含まれています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レンダリング操作</th>
<th align="left">DXGK_RENDERKM_COMMAND メンバー</th>
<th align="left">対応する DXGK_GDIARG_XXX 構造体</th>
<th align="left">対応する DXGK_RENDERKM_OPERATION 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>アルファブレンド</p></td>
<td align="left"><p>AlphaBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>伸縮なしのビットブロック転送</p></td>
<td align="left"><p>BitBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType とアンチエイリアステキストピクセル blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>色の塗りつぶし</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拡張ビット/ブロック転送</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>透明度によるビットブロック転送</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

オペレーティングシステムは、DXGK\_RENDERKM\_コマンドの**オペコード**メンバーを使用して、ディスプレイミニポートドライバーが処理する必要がある特定の GDI ハードウェアアクセラレータレンダリング操作を示します。 **オペコード**メンバーの型は[**DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)で、値はテーブルに表示されます。

また、オペレーティングシステムは、DXGK\_RENDERKM\_COMMAND **Commandsize**メンバーの適切な値を指定します。これは、現在の表示コマンドのサイズをバイト単位で指定します。これは、**オペコード**の値と数値を含みます。コマンド内のサブ四角形の。

透明度によるビットブロック転送を実行するディスプレイアダプターの機能に関する詳細については、DXGK\_GDIARG\_TRANSPARENTBLT に含まれる[**D3DKM\_TRANSPARENTBLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)構造体を参照してください&gt;**Flags**メンバー。

 

 





