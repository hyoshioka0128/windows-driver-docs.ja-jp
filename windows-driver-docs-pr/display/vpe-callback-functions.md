---
title: VPE コールバック関数
description: VPE コールバック関数
ms.assetid: c36e99a5-0657-4945-b5e8-21d875e9d1ec
keywords:
- DirectX VPE サポート WDK DirectDraw, 初期化
- 描画 VPEs WDK DirectDraw, 初期化
- DirectDraw VPEs WDK Windows 2000 の表示、初期化
- 拡張機能のビデオ ポート WDK DirectDraw, 初期化
- VPEs WDK DirectDraw, 初期化
- DirectX VPE 機能を初期化しています
- WDK のビデオ ポートの拡張機能のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 112d04c4bfd61d05bf704e063ab8aaf451d87ad3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376016"
---
# <a name="vpe-callback-functions"></a>VPE コールバック関数


## <span id="ddk_vpe_callback_functions_gg"></span><span id="DDK_VPE_CALLBACK_FUNCTIONS_GG"></span>


次の表には、ディスプレイ ドライバーに実装されているビデオ ポート (VPE) の拡張機能コールバック関数が一覧表示します。 VPE をサポートしているディスプレイ ドライバーが一部 VPE コールバック関数を実装する必要があります。いくつかのハードウェア機能に応じて省略可能です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">VPE コールバック関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport" data-raw-source="[&lt;em&gt;DdVideoPortCanCreate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport)"><em>DdVideoPortCanCreate</em></a></p></td>
<td align="left"><p>ドライバーが指定された説明の DirectDraw VPE オブジェクトをサポートできるかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol" data-raw-source="[&lt;em&gt;DdVideoPortColorControl&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol)"><em>DdVideoPortColorControl</em></a></p></td>
<td align="left"><p>取得または VPE オブジェクトにコントロールの色を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport" data-raw-source="[&lt;em&gt;DdVideoPortCreate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport)"><em>DdVideoPortCreate</em></a></p></td>
<td align="left"><p>DirectDraw VPE オブジェクトが作成されたことをドライバーに通知します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport" data-raw-source="[&lt;em&gt;DdVideoPortDestroy&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport)"><em>DdVideoPortDestroy</em></a></p></td>
<td align="left"><p>DirectDraw に指定した VPE オブジェクトが破棄されたことをドライバーに通知します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip" data-raw-source="[&lt;em&gt;DdVideoPortFlip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip)"><em>DdVideoPortFlip</em></a></p></td>
<td align="left"><p>新しい画面へのデータの書き込みを開始する VPE オブジェクトの原因と、物理、反転を実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth" data-raw-source="[&lt;em&gt;DdVideoPortGetBandwidth&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth)"><em>DdVideoPortGetBandwidth</em></a></p></td>
<td align="left"><p>指定した VPE オブジェクトの出力形式に基づいて、デバイスのフレーム バッファー メモリの帯域幅の制限を報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect" data-raw-source="[&lt;em&gt;DdVideoPortGetConnectInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect)"><em>DdVideoPortGetConnectInfo</em></a></p></td>
<td align="left"><p>指定した VPE オブジェクトでサポートされている接続を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield" data-raw-source="[&lt;em&gt;DdVideoPortGetField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield)"><em>DdVideoPortGetField</em></a></p></td>
<td align="left"><p>インター レースのシグナルの現在のフィールドが偶数か奇数かどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetFlipStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus)"><em>DdVideoPortGetFlipStatus</em></a></p></td>
<td align="left"><p>サーフェスが発生した、最近要求された反転するかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetInputFormats&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats)"><em>DdVideoPortGetInputFormats</em></a></p></td>
<td align="left"><p>DirectDraw VPE オブジェクトが受け入れることができる入力の形式を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline" data-raw-source="[&lt;em&gt;DdVideoPortGetLine&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline)"><em>DdVideoPortGetLine</em></a></p></td>
<td align="left"><p>ビデオ ポートに、ハードウェアの現在の行番号を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetOutputFormats&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats)"><em>DdVideoPortGetOutputFormats</em></a></p></td>
<td align="left"><p>VPE オブジェクトをサポートする出力形式を決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetSignalStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus)"><em>DdVideoPortGetSignalStatus</em></a></p></td>
<td align="left"><p>ハードウェアのビデオ ポートに現在表示されているビデオ信号の状態を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update" data-raw-source="[&lt;em&gt;DdVideoPortUpdate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update)"><em>DdVideoPortUpdate</em></a></p></td>
<td align="left"><p>開始し VPE オブジェクトを停止し、VPE オブジェクトのデータ ストリームを変更します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync" data-raw-source="[&lt;em&gt;DdVideoPortWaitForSync&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync)"><em>DdVideoPortWaitForSync</em></a></p></td>
<td align="left"><p>[次へ] の垂直方向の同期が行われるまで待機します。</p></td>
</tr>
</tbody>
</table>

 

 

 





