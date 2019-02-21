---
title: Windows Display Driver Model (WDDM) の操作フロー
description: Windows Display Driver Model (WDDM) の操作フロー
ms.assetid: 8d2af92c-392a-457d-af9f-796e1050031d
keywords:
- ディスプレイ ドライバー モデル WDK Windows Vista では、操作フロー
- Windows Vista ディスプレイ ドライバー モデル、WDK の操作フロー
- WDK 表示デバイスの表示
- コマンド バッファー WDK の表示、操作フロー
- DMA バッファー WDK の表示、操作フロー
- バッファーの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65ffda8c4276598c2221cb9c5ef845ab8538ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536131"
---
# <a name="windows-display-driver-model-wddm-operation-flow"></a>Windows Display Driver Model (WDDM) の操作フロー


次の図は、表示するため、コンテンツが表示されるため、レンダリング デバイスが作成されたときから発生する Windows 表示 Driver Model (WDDM) 操作の流れを示します。 次のセクションで、シーケンスには、さらに詳しく操作フローがについて説明します。

![wddm 操作のフローを示す図](images/lddmflow.png)

### <a name="span-idcreatingarenderingdevicespanspan-idcreatingarenderingdevicespanspan-idcreatingarenderingdevicespancreating-a-rendering-device"></a><span id="Creating_a_Rendering_Device"></span><span id="creating_a_rendering_device"></span><span id="CREATING_A_RENDERING_DEVICE"></span>レンダリング デバイスを作成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>1.</p></td>
<td align="left"><p>アプリケーションは、レンダリング デバイスを作成する要求、ディスプレイのミニポート ドライバーを受信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559615" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559615)"> <strong>DxgkDdiCreateDevice</strong> </a>呼び出します。 ディスプレイのミニポート ドライバー、塗りつぶされたにポインターを返すことによってダイレクト メモリ アクセス (DMA) を初期化する<a href="https://msdn.microsoft.com/library/windows/hardware/ff561047" data-raw-source="[&lt;strong&gt;DXGK_DEVICEINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561047)"> <strong>DXGK_DEVICEINFO</strong> </a>構造体、 <strong>pInfo</strong> のメンバー<a href="https://msdn.microsoft.com/library/windows/hardware/ff557570" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557570)"><strong>DXGKARG_CREATEDEVICE</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2.</p></td>
<td align="left"><p>場合、ディスプレイのミニポート ドライバーへの呼び出し&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559615" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559615)"> <strong>DxgkDdiCreateDevice</strong> </a>成功すると、マイクロソフトの Direct3D ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出して&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540634" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540634)"> <strong>CreateDevice</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3.</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540634" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540634)"> <strong>CreateDevice</strong> </a>呼び出し、ユーザー モードのディスプレイ ドライバーは呼び出す必要があります明示的に、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568895" data-raw-source="[&lt;strong&gt;pfnCreateContextCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568895)"> <strong>pfnCreateContextCb</strong> </a>関数を作成するには1 つまたは複数のコンテキスト: GPU スレッドで、新しく作成したデバイスを実行します。 Direct3D のランタイム情報が返されます、 <strong>pCommandBuffer</strong>と<strong>CommandBufferSize</strong>のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544143" data-raw-source="[&lt;strong&gt;D3DDDICB_CREATECONTEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544143)"> <strong>D3DDDICB_CREATECONTEXT</strong> </a>コマンド バッファーを初期化するためにします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcreatingsurfacesforadevicespanspan-idcreatingsurfacesforadevicespanspan-idcreatingsurfacesforadevicespancreating-surfaces-for-a-device"></a><span id="Creating_Surfaces_for_a_Device"></span><span id="creating_surfaces_for_a_device"></span><span id="CREATING_SURFACES_FOR_A_DEVICE"></span>デバイスの画面を作成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>4.</p></td>
<td align="left"><p>Direct3D ランタイムがユーザー モードのディスプレイ ドライバーを呼び出すアプリケーションは、レンダリング デバイスのサーフェスを作成する要求、&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540688" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540688)"> <strong>CreateResource</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5.</p></td>
<td align="left"><p>ユーザー モードのディスプレイ ドライバー&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540688" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540688)"> <strong>CreateResource</strong> </a>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568893" data-raw-source="[&lt;strong&gt;pfnAllocateCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568893)"> <strong>pfnAllocateCb</strong> </a>ランタイムによって提供される関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6.</p></td>
<td align="left"><p>ディスプレイのミニポート ドライバーの受信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559606" data-raw-source="[&lt;strong&gt;DxgkDdiCreateAllocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559606)"> <strong>DxgkDdiCreateAllocation</strong> </a>呼び出すには、作成するには、数と割り当ての種類を示します。 <strong>DxgkDdiCreateAllocation</strong>の配列の割り当てに関する情報を返します<a href="https://msdn.microsoft.com/library/windows/hardware/ff560960" data-raw-source="[&lt;strong&gt;DXGK_ALLOCATIONINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560960)"> <strong>DXGK_ALLOCATIONINFO</strong> </a>内の構造体、 <strong>pAllocationInfo</strong>メンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557559" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEALLOCATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557559)"> <strong>DXGKARG_CREATEALLOCATION</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmittingthecommandbuffertokernelmodespanspan-idsubmittingthecommandbuffertokernelmodespanspan-idsubmittingthecommandbuffertokernelmodespansubmitting-the-command-buffer-to-kernel-mode"></a><span id="Submitting_the_Command_Buffer_to_Kernel_Mode"></span><span id="submitting_the_command_buffer_to_kernel_mode"></span><span id="SUBMITTING_THE_COMMAND_BUFFER_TO_KERNEL_MODE"></span>カーネル モードをコマンド バッファーを送信します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>7.</p></td>
<td align="left"><p>Direct3D のランタイム呼び出しユーザー モード アプリケーションが要求を画面に描画するために、表示描画操作に関連するドライバー関数<a href="https://msdn.microsoft.com/library/windows/hardware/ff556151" data-raw-source="[&lt;strong&gt;DrawPrimitive2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556151)"> <strong>DrawPrimitive2</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8.</p></td>
<td align="left"><p>カーネル モードをコマンド バッファーを送信するには、Direct3D ランタイムはユーザー モードのいずれかのディスプレイ ドライバーを呼び出します&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff569176" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569176)"><strong>存在</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff565957" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565957)"><strong>フラッシュ</strong>。</a>関数。 また、ユーザー モードのディスプレイ ドライバーは、コマンド バッファーがいっぱいの場合、コマンド バッファーを送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9.</p></td>
<td align="left"><p>ユーザー モード ドライバーの呼び出しを表示する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568916" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568916)"> <strong>pfnPresentCb</strong> </a>ランタイムによって提供される関数場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff569176" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569176)"><strong>存在</strong></a>が呼び出された、または、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568923" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568923)"> <strong>pfnRenderCb</strong> </a>ランタイムによって提供される関数場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff565957" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565957)"><strong>フラッシュ</strong></a>が呼び出されたコマンド バッファーがいっぱいか。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10.</p></td>
<td align="left"><p>ディスプレイのミニポート ドライバーへの呼び出しを受信する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559743" data-raw-source="[&lt;strong&gt;DxgkDdiPresent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559743)"> <strong>DxgkDdiPresent</strong> </a>機能<a href="https://msdn.microsoft.com/library/windows/hardware/ff568916" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568916)"> <strong>pfnPresentCb</strong> </a>が呼び出されたまたは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559793" data-raw-source="[&lt;strong&gt;DxgkDdiRender&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559793)"> <strong>DxgkDdiRender</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559800" data-raw-source="[&lt;strong&gt;DxgkDdiRenderKm&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559800)"> <strong>DxgkDdiRenderKm</strong> </a>機能<a href="https://msdn.microsoft.com/library/windows/hardware/ff568923" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568923)"> <strong>pfnRenderCb</strong></a>が呼び出されました。 ディスプレイのミニポート ドライバー コマンド バッファーを検証、ハードウェアの DMA バッファーに書き込みます&#39;s 形式、および、サーフェスを記述した割り当て一覧の使用が生成されます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmittingthedmabuffertohardwarespanspan-idsubmittingthedmabuffertohardwarespanspan-idsubmittingthedmabuffertohardwarespansubmitting-the-dma-buffer-to-hardware"></a><span id="Submitting_the_DMA_Buffer_to_Hardware"></span><span id="submitting_the_dma_buffer_to_hardware"></span><span id="SUBMITTING_THE_DMA_BUFFER_TO_HARDWARE"></span>ハードウェアに DMA バッファーを送信します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>11.</p></td>
<td align="left"><p>Microsoft DirectX グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーを呼び出す&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559587" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559587)"> <strong>DxgkDdiBuildPagingBuffer</strong> </a> DMA バッファー、ページングのバッファーと呼ばれる特殊な目的を作成する関数GPU からアクセス可能なメモリとの間の割り当てリストで指定した割り当てを移動するとします。</p>
<div class="alert">
<strong>注</strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff559587" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559587)"><strong>DxgkDdiBuildPagingBuffer</strong> </a>のすべてのフレームは呼び出されません。  
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>12.</p></td>
<td align="left"><p>DirectX グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーを呼び出す&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff560790" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560790)"> <strong>DxgkDdiSubmitCommand</strong> </a>関数 GPU 実行単位にページング バッファーをキューに登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13.</p></td>
<td align="left"><p>DirectX グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーを呼び出す&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559737" data-raw-source="[&lt;strong&gt;DxgkDdiPatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559737)"> <strong>DxgkDdiPatch</strong> </a> DMA バッファー内のリソースへの物理アドレスを割り当てる関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14.</p></td>
<td align="left"><p>DirectX グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーを呼び出す&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff560790" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560790)"> <strong>DxgkDdiSubmitCommand</strong> </a>関数 DMA バッファーを GPU の実行の単位をキューに登録します。 GPU に送信される各 DMA バッファーには、数値、フェンスの識別子が含まれています。 GPU では、DMA バッファーの処理が完了すると、GPU は、割り込みを生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>15.</p></td>
<td align="left"><p>ディスプレイのミニポート ドライバーは、割り込みの通知、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559680" data-raw-source="[&lt;strong&gt;DxgkDdiInterruptRoutine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559680)"> <strong>DxgkDdiInterruptRoutine</strong> </a>関数。 ディスプレイのミニポート ドライバーから読み取ら GPU、完了した DMA バッファーをフェンスの識別子。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16.</p></td>
<td align="left"><p>ディスプレイのミニポート ドライバーを呼び出す必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559545" data-raw-source="[&lt;strong&gt;DxgkCbNotifyInterrupt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559545)"> <strong>DxgkCbNotifyInterrupt</strong> </a> DMA バッファーが完了した DirectX グラフィックスのカーネル サブシステムに通知します。 ディスプレイのミニポート ドライバーに呼び出す必要がありますも、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559559" data-raw-source="[&lt;strong&gt;DxgkCbQueueDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559559)"> <strong>DxgkCbQueueDpc</strong> </a>関数遅延プロシージャ呼び出し (DPC) をキューに登録します。</p></td>
</tr>
</tbody>
</table>

 

 

 





