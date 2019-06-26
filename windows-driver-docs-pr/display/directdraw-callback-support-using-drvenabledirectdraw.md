---
title: DrvEnableDirectDraw を使用した DirectDraw コールバックのサポート
description: DrvEnableDirectDraw を使用した DirectDraw コールバックのサポート
ms.assetid: 74caab2b-6976-411a-97af-7c94b0c12fa0
keywords:
- Windows 2000、Windows 2000 の WDK 表示 DirectDraw ドライバーの初期化
- WDK DirectDraw のコールバック関数
- DrvEnableDirectDraw
- DirectDraw ドライバー WDK Windows 2000 の表示、コールバック関数の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d711257a6e69c9851fe00a79ce6f69faaa249c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384849"
---
# <a name="directdraw-callback-support-using-drvenabledirectdraw"></a>DrvEnableDirectDraw を使用した DirectDraw コールバックのサポート


## <span id="ddk_directdraw_callback_support_using_drvenabledirectdraw_gg"></span><span id="DDK_DIRECTDRAW_CALLBACK_SUPPORT_USING_DRVENABLEDIRECTDRAW_GG"></span>


ディスプレイ ドライバーが実装できる、 [ **DrvEnableDirectDraw** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledirectdraw)関数をさまざまな DirectDraw のコールバック サポートを示します。 サポートを示すために、ドライバーがへのポインターを返します、 [ **DD\_コールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks)、 [ **DD\_SURFACECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)、および[ **DD\_PALETTECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks)内の構造体、 *pCallBacks*、 *pSurfaceCallBacks*、および*pPaletteCallBacks*パラメーター。

ドライバーのメンバーを設定します、 [ **DD\_コールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_callbacks)構造体を次のコールバック関数をサポートしていることを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)" data-raw-source="[&lt;em&gt;DdCanCreateSurface&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))"><em>DdCanCreateSurface</em></a></p></td>
<td align="left"><p>ドライバーが表面の指定された説明のサーフェスを作成できるかどうかを示す値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette" data-raw-source="[&lt;em&gt;DdCreatePalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createpalette)"><em>DdCreatePalette</em></a></p></td>
<td align="left"><p>指定した DirectDraw オブジェクト DirectDrawPalette オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)" data-raw-source="[&lt;em&gt;DdCreateSurface&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))"><em>DdCreateSurface</em></a></p></td>
<td align="left"><p>DirectDraw surface を作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline" data-raw-source="[&lt;em&gt;DdGetScanLine&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline)"><em>DdGetScanLine</em></a></p></td>
<td align="left"><p>現在の行の物理的なスキャンの数を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory" data-raw-source="[&lt;em&gt;DdMapMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)"><em>DdMapMemory</em></a></p></td>
<td align="left"><p>マップのアプリケーションが変更可能なアドレス空間の指定されたプロセスがユーザー モードにフレーム バッファーの一部またはメモリの割り当てを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank" data-raw-source="[&lt;em&gt;DdWaitForVerticalBlank&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_waitforverticalblank)"><em>DdWaitForVerticalBlank</em></a></p></td>
<td align="left"><p>デバイスの垂直方向の空白の状態を返します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーのメンバーを設定します、 [ **DD\_SURFACECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)構造体を次のコールバック関数をサポートしていることを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface" data-raw-source="[&lt;em&gt;DdAddAttachedSurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_addattachedsurface)"><em>DdAddAttachedSurface</em></a></p></td>
<td align="left"><p>別の画面には、サーフェスをアタッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt" data-raw-source="[&lt;em&gt;DdBlt&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)"><em>DdBlt</em></a></p></td>
<td align="left"><p>ソース画面から宛先表面へのデータの表示のビット ブロック転送 (blt) を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface" data-raw-source="[&lt;em&gt;DdDestroySurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)"><em>DdDestroySurface</em></a></p></td>
<td align="left"><p>DirectDraw surface を破棄します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip" data-raw-source="[&lt;em&gt;DdFlip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)"><em>DdFlip</em></a></p></td>
<td align="left"><p>により、プライマリのサーフェスをターゲット サーフェスと非プライマリのサーフェイスに現在の画面に関連付けられたサーフェスのメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus" data-raw-source="[&lt;em&gt;DdGetBltStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus)"><em>DdGetBltStatus</em></a></p></td>
<td align="left"><p>指定した表面の blt 状態を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus" data-raw-source="[&lt;em&gt;DdGetFlipStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getflipstatus)"><em>DdGetFlipStatus</em></a></p></td>
<td align="left"><p>サーフェスが発生した、最近要求された反転するかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock" data-raw-source="[&lt;em&gt;DdLock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)"><em>DdLock</em></a></p></td>
<td align="left"><p>表面のメモリの指定された領域をロックし、サーフェイスに関連付けられたメモリ ブロックへの有効なポインターを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey" data-raw-source="[&lt;em&gt;DdSetColorKey&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setcolorkey)"><em>DdSetColorKey</em></a></p></td>
<td align="left"><p>指定した表面の色のキー値を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition" data-raw-source="[&lt;em&gt;DdSetOverlayPosition&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setoverlayposition)"><em>DdSetOverlayPosition</em></a></p></td>
<td align="left"><p>オーバーレイの位置を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette" data-raw-source="[&lt;em&gt;DdSetPalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_setpalette)"><em>DdSetPalette</em></a></p></td>
<td align="left"><p>指定した表面にパレットをアタッチします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock" data-raw-source="[&lt;em&gt;DdUnlock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)"><em>DdUnlock</em></a></p></td>
<td align="left"><p>指定した表面に保持されているロックを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay" data-raw-source="[&lt;em&gt;DdUpdateOverlay&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay)"><em>DdUpdateOverlay</em></a></p></td>
<td align="left"><p>位置を変更またはオーバーレイ、画面の表示属性を変更します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーのメンバーを設定します、 [ **DD\_PALETTECALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_palettecallbacks)構造体を次のコールバック関数をサポートしていることを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette" data-raw-source="[&lt;em&gt;DdDestroyPalette&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_destroypalette)"><em>DdDestroyPalette</em></a></p></td>
<td align="left"><p>指定したパレットを破棄します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries" data-raw-source="[&lt;em&gt;DdSetEntries&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_palcb_setentries)"><em>DdSetEntries</em></a></p></td>
<td align="left"><p>指定のパレットのパレット エントリを更新します。</p></td>
</tr>
</tbody>
</table>

 

 

 





