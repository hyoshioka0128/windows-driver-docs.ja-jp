---
title: カーネル モード ビデオ トランスポートのコールバック関数
description: カーネル モード ビデオ トランスポートのコールバック関数
ms.assetid: 1edd5b68-91da-4846-87bd-6fcabb9e5abf
keywords:
- DxApi ミニポート ドライバー WDK DirectDraw、カーネル モードのビデオ トランスポート コールバック関数
- カーネル モードのビデオ トランスポート WDK DirectDraw、コールバック関数
- コールバック関数 WDK のカーネル モードのビデオ トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f19634e6823db1d54eb6ff39b1d13e934783d68a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363096"
---
# <a name="kernel-mode-video-transport-callback-functions"></a>カーネル モード ビデオ トランスポートのコールバック関数


## <span id="ddk_kernel_mode_video_transport_callback_functions_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_CALLBACK_FUNCTIONS_GG"></span>


次の表には、ビデオのミニポート ドライバーに実装されているカーネル モードのビデオ トランスポート コールバック関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DxApi コールバック関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557409" data-raw-source="[&lt;em&gt;DxBobNextField&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557409)"><em>DxBobNextField</em></a></p></td>
<td align="left"><p>インターリーブ データの次のフィールドを bobs します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557413" data-raw-source="[&lt;em&gt;DxEnableIRQ&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557413)"><em>DxEnableIRQ</em></a></p></td>
<td align="left"><p>Irq を有効または無効にする必要がありますミニポート ドライバーに指示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557417" data-raw-source="[&lt;em&gt;DxFlipOverlay&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557417)"><em>DxFlipOverlay</em></a></p></td>
<td align="left"><p>オーバーレイを反転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557420" data-raw-source="[&lt;em&gt;DxFlipVideoPort&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557420)"><em>DxFlipVideoPort</em></a></p></td>
<td align="left"><p>ビデオ ポートの拡張機能 (VPE) オブジェクトを反転します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557427" data-raw-source="[&lt;em&gt;DxGetCurrentAutoflip&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557427)"><em>DxGetCurrentAutoflip</em></a></p></td>
<td align="left"><p>どの画面がビデオ データ キャプチャのための現在のフィールドを受信して決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557428" data-raw-source="[&lt;em&gt;DxGetIRQInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557428)"><em>DxGetIRQInfo</em></a></p></td>
<td align="left"><p>ドライバーが割り込み要求を管理することを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557431" data-raw-source="[&lt;em&gt;DxGetPolarity&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557431)"><em>DxGetPolarity</em></a></p></td>
<td align="left"><p>VPE オブジェクトによって書き込まれている現在のフィールドの極性 (偶数か奇数) を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557437" data-raw-source="[&lt;em&gt;DxGetPreviousAutoflip&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557437)"><em>DxGetPreviousAutoflip</em></a></p></td>
<td align="left"><p>どの画面が、前のフィールドのキャプチャのためのビデオ データを受信したかを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557438" data-raw-source="[&lt;em&gt;DxGetTransferStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557438)"><em>DxGetTransferStatus</em></a></p></td>
<td align="left"><p>どのハードウェア バスを決定します。 マスターが完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562880" data-raw-source="[&lt;em&gt;DxLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562880)"><em>DxLock</em></a></p></td>
<td align="left"><p>フレーム バッファーをロックするは、アクセスできるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562882" data-raw-source="[&lt;em&gt;DxSetState&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562882)"><em>DxSetState</em></a></p></td>
<td align="left"><p>モードに bob モードから切り替えまたはその逆です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562885" data-raw-source="[&lt;em&gt;DxSkipNextField&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562885)"><em>DxSkipNextField</em></a></p></td>
<td align="left"><p>スキップまたは次のフィールドを再び有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562887" data-raw-source="[&lt;em&gt;DxTransfer&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562887)"><em>DxTransfer</em></a></p></td>
<td align="left"><p>バス マスターのサーフェスからメモリ記述子のリスト (MDL) で指定されたバッファーへのデータ。</p></td>
</tr>
</tbody>
</table>

 

 

 





