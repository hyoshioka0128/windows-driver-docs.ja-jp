---
title: GDI ハードウェア アクセラレータによるレンダリング操作を指定します。
description: GDI ハードウェア アクセラレータによるレンダリング操作を指定します。
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- GDI ハードウェア アクセラレータを WDK を表示して操作を表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e67aa705c8eca6d9243cccd72fc4ed8f7661a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532521"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>GDI ハードウェア アクセラレータによるレンダリング操作を指定します。


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


ときに、 [ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)関数が呼び出されると、オペレーティング システムを使用して実行する GDI ハードウェア アクセラレータによるレンダリング操作の種類を指定します、 *pRenderKmArgs*パラメーター。 DirectX グラフィックスのカーネル サブシステムのディスプレイ ポート ドライバー (*Dxgkrnl.sys*) 設定、 *pRenderKmArgs*-&gt;**pCommand**メンバー可変サイズの配列が含まれたコマンド バッファーを指す[ **DXGK\_RENDERKM\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff562026)構造体。 また、設定、 *pRenderKmArgs*-&gt;**pCommandLength**メンバー (バイト単位) をコマンド バッファーのサイズにします。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561074" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561074)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>伸縮しないでビット ブロック転送</p></td>
<td align="left"><p>Bitblt 関数</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561079" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561079)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType とアンチ エイリアス化テキスト ピクセル blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561082" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561082)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>色の塗りつぶし</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561083" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561083)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビット ブロック転送を拡大</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561089" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561089)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>透過性のビット ブロック転送</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561091" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561091)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

オペレーティング システムの使用、**オペコード**DXGK のメンバー\_RENDERKM\_ディスプレイのミニポート ドライバーを処理する必要がある特定の GDI ハードウェア アクセラレータによるレンダリング操作を示すコマンド。 **オペコード**型のメンバーは、 [ **DXGK\_RENDERKM\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff562029)表に示した値を使用します。

オペレーティング システムが、DXGK の適切な値を指定することも\_RENDERKM\_コマンド**CommandSize**メンバーで、バイト単位の値を含む、現在のレンダリング コマンドのサイズを指定します。**オペコード**とコマンドのサブ四角形の数。

透過性でビット ブロック転送を実行するディスプレイ アダプターの機能に関する情報を提供するさらに、 [ **D3DKM\_TRANSPARENTBLTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff548468)に含まれている構造体DXGK\_GDIARG\_TRANSPARENTBLT -&gt;**フラグ**メンバー。

 

 





