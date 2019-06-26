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
ms.openlocfilehash: e654c2248c786d03963de02111ce2635cd726175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372900"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_bobnextfield" data-raw-source="[&lt;em&gt;DxBobNextField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_bobnextfield)"><em>DxBobNextField</em></a></p></td>
<td align="left"><p>インターリーブ データの次のフィールドを bobs します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq" data-raw-source="[&lt;em&gt;DxEnableIRQ&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq)"><em>DxEnableIRQ</em></a></p></td>
<td align="left"><p>Irq を有効または無効にする必要がありますミニポート ドライバーに指示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipoverlay" data-raw-source="[&lt;em&gt;DxFlipOverlay&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipoverlay)"><em>DxFlipOverlay</em></a></p></td>
<td align="left"><p>オーバーレイを反転します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipvideoport" data-raw-source="[&lt;em&gt;DxFlipVideoPort&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipvideoport)"><em>DxFlipVideoPort</em></a></p></td>
<td align="left"><p>ビデオ ポートの拡張機能 (VPE) オブジェクトを反転します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getcurrentautoflip" data-raw-source="[&lt;em&gt;DxGetCurrentAutoflip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getcurrentautoflip)"><em>DxGetCurrentAutoflip</em></a></p></td>
<td align="left"><p>どの画面がビデオ データ キャプチャのための現在のフィールドを受信して決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getirqinfo" data-raw-source="[&lt;em&gt;DxGetIRQInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getirqinfo)"><em>DxGetIRQInfo</em></a></p></td>
<td align="left"><p>ドライバーが割り込み要求を管理することを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpolarity" data-raw-source="[&lt;em&gt;DxGetPolarity&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpolarity)"><em>DxGetPolarity</em></a></p></td>
<td align="left"><p>VPE オブジェクトによって書き込まれている現在のフィールドの極性 (偶数か奇数) を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpreviousautoflip" data-raw-source="[&lt;em&gt;DxGetPreviousAutoflip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpreviousautoflip)"><em>DxGetPreviousAutoflip</em></a></p></td>
<td align="left"><p>どの画面が、前のフィールドのキャプチャのためのビデオ データを受信したかを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus" data-raw-source="[&lt;em&gt;DxGetTransferStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)"><em>DxGetTransferStatus</em></a></p></td>
<td align="left"><p>どのハードウェア バスを決定します。 マスターが完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_lock" data-raw-source="[&lt;em&gt;DxLock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_lock)"><em>DxLock</em></a></p></td>
<td align="left"><p>フレーム バッファーをロックするは、アクセスできるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_setstate" data-raw-source="[&lt;em&gt;DxSetState&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_setstate)"><em>DxSetState</em></a></p></td>
<td align="left"><p>モードに bob モードから切り替えまたはその逆です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_skipnextfield" data-raw-source="[&lt;em&gt;DxSkipNextField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_skipnextfield)"><em>DxSkipNextField</em></a></p></td>
<td align="left"><p>スキップまたは次のフィールドを再び有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer" data-raw-source="[&lt;em&gt;DxTransfer&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer)"><em>DxTransfer</em></a></p></td>
<td align="left"><p>バス マスターのサーフェスからメモリ記述子のリスト (MDL) で指定されたバッファーへのデータ。</p></td>
</tr>
</tbody>
</table>

 

 

 





