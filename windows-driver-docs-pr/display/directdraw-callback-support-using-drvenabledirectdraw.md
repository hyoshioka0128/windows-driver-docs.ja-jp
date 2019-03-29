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
ms.openlocfilehash: 2e58538d0ad460b5d962354aad57b2e8f7f59775
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569697"
---
# <a name="directdraw-callback-support-using-drvenabledirectdraw"></a>DrvEnableDirectDraw を使用した DirectDraw コールバックのサポート


## <span id="ddk_directdraw_callback_support_using_drvenabledirectdraw_gg"></span><span id="DDK_DIRECTDRAW_CALLBACK_SUPPORT_USING_DRVENABLEDIRECTDRAW_GG"></span>


ディスプレイ ドライバーが実装できる、 [ **DrvEnableDirectDraw** ](https://msdn.microsoft.com/library/windows/hardware/ff556208)関数をさまざまな DirectDraw のコールバック サポートを示します。 サポートを示すために、ドライバーがへのポインターを返します、 [ **DD\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff550485)、 [ **DD\_SURFACECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551721)、および[ **DD\_PALETTECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551681)内の構造体、 *pCallBacks*、 *pSurfaceCallBacks*、および*pPaletteCallBacks*パラメーター。

ドライバーのメンバーを設定します、 [ **DD\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff550485)構造体を次のコールバック関数をサポートしていることを示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549213" data-raw-source="[&lt;em&gt;DdCanCreateSurface&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549213)"><em>DdCanCreateSurface</em></a></p></td>
<td align="left"><p>ドライバーが表面の指定された説明のサーフェスを作成できるかどうかを示す値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549254" data-raw-source="[&lt;em&gt;DdCreatePalette&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549254)"><em>DdCreatePalette</em></a></p></td>
<td align="left"><p>指定した DirectDraw オブジェクト DirectDrawPalette オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549263" data-raw-source="[&lt;em&gt;DdCreateSurface&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549263)"><em>DdCreateSurface</em></a></p></td>
<td align="left"><p>DirectDraw surface を作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549497" data-raw-source="[&lt;em&gt;DdGetScanLine&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549497)"><em>DdGetScanLine</em></a></p></td>
<td align="left"><p>現在の行の物理的なスキャンの数を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549641" data-raw-source="[&lt;em&gt;DdMapMemory&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549641)"><em>DdMapMemory</em></a></p></td>
<td align="left"><p>マップのアプリケーションが変更可能なアドレス空間の指定されたプロセスがユーザー モードにフレーム バッファーの一部またはメモリの割り当てを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550457" data-raw-source="[&lt;em&gt;DdWaitForVerticalBlank&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550457)"><em>DdWaitForVerticalBlank</em></a></p></td>
<td align="left"><p>デバイスの垂直方向の空白の状態を返します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーのメンバーを設定します、 [ **DD\_SURFACECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551721)構造体を次のコールバック関数をサポートしていることを示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549194" data-raw-source="[&lt;em&gt;DdAddAttachedSurface&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549194)"><em>DdAddAttachedSurface</em></a></p></td>
<td align="left"><p>別の画面には、サーフェスをアタッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549205" data-raw-source="[&lt;em&gt;DdBlt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549205)"><em>DdBlt</em></a></p></td>
<td align="left"><p>ソース画面から宛先表面へのデータの表示のビット ブロック転送 (blt) を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549281" data-raw-source="[&lt;em&gt;DdDestroySurface&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549281)"><em>DdDestroySurface</em></a></p></td>
<td align="left"><p>DirectDraw surface を破棄します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549306" data-raw-source="[&lt;em&gt;DdFlip&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549306)"><em>DdFlip</em></a></p></td>
<td align="left"><p>により、プライマリのサーフェスをターゲット サーフェスと非プライマリのサーフェイスに現在の画面に関連付けられたサーフェスのメモリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549385" data-raw-source="[&lt;em&gt;DdGetBltStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549385)"><em>DdGetBltStatus</em></a></p></td>
<td align="left"><p>指定した表面の blt 状態を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549429" data-raw-source="[&lt;em&gt;DdGetFlipStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549429)"><em>DdGetFlipStatus</em></a></p></td>
<td align="left"><p>サーフェスが発生した、最近要求された反転するかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549599" data-raw-source="[&lt;em&gt;DdLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549599)"><em>DdLock</em></a></p></td>
<td align="left"><p>表面のメモリの指定された領域をロックし、サーフェイスに関連付けられたメモリ ブロックへの有効なポインターを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550301" data-raw-source="[&lt;em&gt;DdSetColorKey&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550301)"><em>DdSetColorKey</em></a></p></td>
<td align="left"><p>指定した表面の色のキー値を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550311" data-raw-source="[&lt;em&gt;DdSetOverlayPosition&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550311)"><em>DdSetOverlayPosition</em></a></p></td>
<td align="left"><p>オーバーレイの位置を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550312" data-raw-source="[&lt;em&gt;DdSetPalette&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550312)"><em>DdSetPalette</em></a></p></td>
<td align="left"><p>指定した表面にパレットをアタッチします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550365" data-raw-source="[&lt;em&gt;DdUnlock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550365)"><em>DdUnlock</em></a></p></td>
<td align="left"><p>指定した表面に保持されているロックを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550369" data-raw-source="[&lt;em&gt;DdUpdateOverlay&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550369)"><em>DdUpdateOverlay</em></a></p></td>
<td align="left"><p>位置を変更またはオーバーレイ、画面の表示属性を変更します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーのメンバーを設定します、 [ **DD\_PALETTECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551681)構造体を次のコールバック関数をサポートしていることを示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549276" data-raw-source="[&lt;em&gt;DdDestroyPalette&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549276)"><em>DdDestroyPalette</em></a></p></td>
<td align="left"><p>指定したパレットを破棄します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550302" data-raw-source="[&lt;em&gt;DdSetEntries&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550302)"><em>DdSetEntries</em></a></p></td>
<td align="left"><p>指定のパレットのパレット エントリを更新します。</p></td>
</tr>
</tbody>
</table>

 

 

 





