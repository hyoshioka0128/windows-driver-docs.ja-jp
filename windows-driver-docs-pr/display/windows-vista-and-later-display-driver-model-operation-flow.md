---
title: Windows Display Driver Model (WDDM) の操作フロー
description: Windows Display Driver Model (WDDM) の操作フロー
ms.assetid: 8d2af92c-392a-457d-af9f-796e1050031d
keywords:
- ディスプレイドライバーモデル WDK Windows Vista、操作フロー
- Windows Vista display driver model WDK、operation flow
- レンダリングデバイスの WDK ディスプレイ
- コマンドバッファー WDK 表示、操作フロー
- DMA バッファー WDK 表示、操作フロー
- WDK のバッファーの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38dc908189b2063bc788cb24377b5859835ede7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829133"
---
# <a name="windows-display-driver-model-wddm-operation-flow"></a>Windows Display Driver Model (WDDM) の操作フロー


次の図は、ディスプレイにコンテンツを表示するときに、レンダリングデバイスが作成されたときに発生する Windows Display Driver Model (WDDM) 操作のフローを示しています。 以降のセクションでは、操作フローの詳細について説明します。

![wddm 操作フローを示す図](images/lddmflow.png)

### <a name="span-idcreating_a_rendering_devicespanspan-idcreating_a_rendering_devicespanspan-idcreating_a_rendering_devicespancreating-a-rendering-device"></a><span id="Creating_a_Rendering_Device"></span><span id="creating_a_rendering_device"></span><span id="CREATING_A_RENDERING_DEVICE"></span>レンダリングデバイスの作成

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>1.</p></td>
<td align="left"><p>アプリケーションがレンダリングデバイスの作成を要求すると、表示ミニポートドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)"><strong>DxgkDdiCreateDevice</strong></a>呼び出しを受け取ります。 ディスプレイミニポートドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice)"><strong>DXGKARG_CREATEDEVICE</strong></a>構造体の<strong>pInfo</strong>メンバーの塗りつぶされた<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo" data-raw-source="[&lt;strong&gt;DXGK_DEVICEINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)"><strong>DXGK_DEVICEINFO</strong></a>構造体へのポインターを返すことによって、ダイレクトメモリアクセス (DMA) を初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2.</p></td>
<td align="left"><p>ディスプレイミニポートドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)"><strong>DxgkDdiCreateDevice</strong></a>の呼び出しが成功すると、Microsoft Direct3D ランタイムはユーザーモードの表示ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)"><strong>CreateDevice</strong></a>関数を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3.</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)"><strong>CreateDevice</strong></a>の呼び出しでは、ユーザーモードの表示ドライバーが<a href="https://docs.microsoft.com/previous-versions/ff568895(v=vs.85)" data-raw-source="[&lt;strong&gt;pfnCreateContextCb&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff568895(v=vs.85))"><strong>pfnCreateContextCb</strong></a>関数を明示的に呼び出して、1つまたは複数のコンテキストを作成する必要があります。これは、新しく作成されたデバイスで GPU スレッドが実行されます。 Direct3D ランタイムは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createcontext" data-raw-source="[&lt;strong&gt;D3DDDICB_CREATECONTEXT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createcontext)"><strong>D3DDDICB_CREATECONTEXT</strong></a>構造体の<strong>pcommandbuffer</strong>および<strong>commandbuffersize</strong>のメンバーにある情報を返して、コマンドバッファーを初期化します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcreating_surfaces_for_a_devicespanspan-idcreating_surfaces_for_a_devicespanspan-idcreating_surfaces_for_a_devicespancreating-surfaces-for-a-device"></a><span id="Creating_Surfaces_for_a_Device"></span><span id="creating_surfaces_for_a_device"></span><span id="CREATING_SURFACES_FOR_A_DEVICE"></span>デバイス用のサーフェイスの作成

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>4.</p></td>
<td align="left"><p>アプリケーションがレンダリングデバイスのサーフェイスの作成を要求すると、Direct3D ランタイムはユーザーモードの display ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)"><strong>Createresource</strong></a>関数を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5.</p></td>
<td align="left"><p>ユーザーモードのディスプレイドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)"><strong>Createresource</strong></a>は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb" data-raw-source="[&lt;strong&gt;pfnAllocateCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)"><strong>Pfnallocatecb</strong></a>ランタイムによって提供される関数を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6.</p></td>
<td align="left"><p>表示ミニポートドライバーは、作成する割り当ての数と種類を示す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation" data-raw-source="[&lt;strong&gt;DxgkDdiCreateAllocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)"><strong>DxgkDdiCreateAllocation</strong></a>呼び出しを受信します。 <strong>DxgkDdiCreateAllocation</strong> <strong>は、</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEALLOCATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)"><strong>DXGKARG_CREATEALLOCATION</strong></a>構造体の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo" data-raw-source="[&lt;strong&gt;DXGK_ALLOCATIONINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)"><strong>DXGK_ALLOCATIONINFO</strong></a>構造体の配列における割り当てに関する情報を返します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmitting_the_command_buffer_to_kernel_modespanspan-idsubmitting_the_command_buffer_to_kernel_modespanspan-idsubmitting_the_command_buffer_to_kernel_modespansubmitting-the-command-buffer-to-kernel-mode"></a><span id="Submitting_the_Command_Buffer_to_Kernel_Mode"></span><span id="submitting_the_command_buffer_to_kernel_mode"></span><span id="SUBMITTING_THE_COMMAND_BUFFER_TO_KERNEL_MODE"></span>コマンドバッファーをカーネルモードに送信しています

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>7.</p></td>
<td align="left"><p>アプリケーションがサーフェイスへの描画を要求すると、Direct3D ランタイムは、描画操作に関連するユーザーモードの display driver 関数 (たとえば、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawprimitive2" data-raw-source="[&lt;strong&gt;DrawPrimitive2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawprimitive2)"><strong>DrawPrimitive2</strong></a>) を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8.</p></td>
<td align="left"><p>コマンドバッファーをカーネルモードに送信するために、Direct3D ランタイムは、ユーザーモードの display ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)"><strong>Present</strong></a>関数または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)"><strong>Flush</strong></a>関数を呼び出します。 また、コマンドバッファーがいっぱいになった場合は、ユーザーモードの表示ドライバーによってコマンドバッファーが送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9.</p></td>
<td align="left"><p>ユーザーモード表示ドライバーは、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)"><strong>現在</strong></a>が呼び出された場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)"><strong>Pfnpresent cb</strong></a>ランタイムが指定した関数を呼び出します。または、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)"><strong>Flush</strong></a>が呼び出された場合、またはコマンドバッファーがいっぱいの場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)"><strong>pfnpresentcb</strong></a>ランタイムによって指定された関数を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10.</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)"><strong>PfnDxgkDdiPresent cb</strong></a>が呼び出された場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present" data-raw-source="[&lt;strong&gt;DxgkDdiPresent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)"></a> 、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render" data-raw-source="[&lt;strong&gt;DxgkDdiRender&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)"><strong>DxgkDdiRender</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm" data-raw-source="[&lt;strong&gt;DxgkDdiRenderKm&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)"><strong>DxgkDdiRenderKm</strong></a>関数が呼び出され<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)"><strong>た場合、</strong></a>表示ミニポートドライバーは、その関数の呼び出しを受け取ります。 ミニミニポートドライバーは、コマンドバッファーを検証し、ハードウェアの形式で DMA バッファーに書き込み、使用されているサーフェスを示す割り当てリストを生成します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmitting_the_dma_buffer_to_hardwarespanspan-idsubmitting_the_dma_buffer_to_hardwarespanspan-idsubmitting_the_dma_buffer_to_hardwarespansubmitting-the-dma-buffer-to-hardware"></a><span id="Submitting_the_DMA_Buffer_to_Hardware"></span><span id="submitting_the_dma_buffer_to_hardware"></span><span id="SUBMITTING_THE_DMA_BUFFER_TO_HARDWARE"></span>DMA バッファーをハードウェアに送信する

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>11.</p></td>
<td align="left"><p>Microsoft DirectX graphics kernel サブシステムは、ディスプレイミニポートドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)"><strong>DxgkDdiBuildPagingBuffer</strong></a>関数を呼び出して、割り当てリストで指定された割り当てをとに移動する、ページングバッファーと呼ばれる特殊な目的の DMA バッファーを作成します。GPU のアクセス可能なメモリから。</p>
<div class="alert">
<strong>注</strong>  <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)"><strong>DxgkDdiBuildPagingBuffer</strong></a>は、すべてのフレームに対して呼び出されません。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>12.</p></td>
<td align="left"><p>DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)"><strong>DxgkDdiSubmitCommand</strong></a>関数を呼び出して、GPU 実行単位へのページングバッファーをキューに配置します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13.</p></td>
<td align="left"><p>DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch" data-raw-source="[&lt;strong&gt;DxgkDdiPatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)"><strong>DxgkDdiPatch</strong></a>関数を呼び出して、DMA バッファー内のリソースに物理アドレスを割り当てます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14.</p></td>
<td align="left"><p>DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)"><strong>DxgkDdiSubmitCommand</strong></a>関数を呼び出して、GPU 実行単位に対して DMA バッファーをキューに配置します。 GPU に送信される各 DMA バッファーには、フェンス識別子 (数値) が含まれています。 GPU が DMA バッファーの処理を終了すると、GPU によって割り込みが生成されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>15.</p></td>
<td align="left"><p>ディスプレイミニポートドライバーには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine" data-raw-source="[&lt;strong&gt;DxgkDdiInterruptRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)"><strong>DxgkDdiInterruptRoutine</strong></a>関数の割り込みが通知されます。 表示ミニポートドライバーは、完了したばかりの DMA バッファーのフェンス識別子を GPU から読み取る必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16.</p></td>
<td align="left"><p>ディスプレイミニポートドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt" data-raw-source="[&lt;strong&gt;DxgkCbNotifyInterrupt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)"><strong>Dxgkcbnotifyinterrupt</strong></a>関数を呼び出して、DMA バッファーが完了したことを DirectX グラフィックスカーネルサブシステムに通知する必要があります。 また、ディスプレイミニポートドライバーは、遅延プロシージャ呼び出し (DPC) をキューにするために<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc" data-raw-source="[&lt;strong&gt;DxgkCbQueueDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)"><strong>DxgkCbQueueDpc</strong></a>関数を呼び出す必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





