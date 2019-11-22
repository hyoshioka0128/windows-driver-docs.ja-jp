---
title: GPU プリエンプション
description: 新しい GPU プリエンプションモデルは、Windows 8 以降で使用できます。
ms.assetid: 9382786E-2E1E-408F-A9E9-04EEEA1CC34A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c68650e59950e295258f9a8a5d12c6241a625cdc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839673"
---
# <a name="gpu-preemption"></a>GPU プリエンプション


新しい GPU プリエンプションモデルは、Windows 8 以降で使用できます。 このモデルでは、オペレーティングシステムで GPU ダイレクトメモリアクセス (DMA) パケットのプリエンプションを無効にすることができなくなりました。また、[タイムアウト検出と復旧 (TDR)](timeout-detection-and-recovery.md)プロセスが開始される前に、プリエンプト要求が gpu に送信されることを保証します.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows Display Driver Model (WDDM) の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装—完全なグラフィックスとレンダーのみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>デバイス...プリエンプションテスト</strong></p>
<p><strong>デバイス...FlipOnVSyncMmIo</strong></p></td>
</tr>
</tbody>
</table>

 

長時間実行されているパケットが正常に割り込まれない場合は、デスクトップウィンドウマネージャー (DWM) で必要な作業など、優先順位の高い GPU 作業が遅延する可能性があります。これにより、ウィンドウの切り替えとアニメーションの実行中に問題が発生します。 また、横取りできない長時間実行されている GPU パケットは、TDR プロセスによって GPU が繰り返しリセットされる可能性があり、最終的にシステムのバグチェックが発生する可能性があります。

**注**   すべての WDDM 1.2 表示ミニポートドライバーで、Windows 8 のプリエンプションモデルがサポートされている必要があります。 ただし、操作中は、WDDM 1.2 ドライバーが Windows 8 のプリエンプションモデルを拒否し、Microsoft DirectX graphics カーネルサブシステムスケジューラによって Windows 7 の動作を保持することもできます。

 

## <a name="span-idgpu_preemption_device_driver_interfaces__ddis_spanspan-idgpu_preemption_device_driver_interfaces__ddis_spanspan-idgpu_preemption_device_driver_interfaces__ddis_spangpu-preemption-device-driver-interfaces-ddis"></a><span id="GPU_preemption_device_driver_interfaces__DDIs_"></span><span id="gpu_preemption_device_driver_interfaces__ddis_"></span><span id="GPU_PREEMPTION_DEVICE_DRIVER_INTERFACES__DDIS_"></span>GPU プリエンプションデバイスドライバーインターフェイス (DDIs)


Windows 8 GPU プリエンプションモデルを実装するために、ディスプレイミニポートドライバーでは、次のデバイスドライバーインターフェイス (DDIs) を使用できます。

-   [*DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)
-   [*DxgkCbDestroyContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation)
-   [*Pfnset優先度 Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setprioritycb)
-   [Dxgkrnl インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [**DXGKRNL\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgkrnl_interface)
-   [**D3DKMDT\_計算\_プリエンプション\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity)
-   [**D3DKMDT\_グラフィックス\_プリエンプション\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity)
-   [**D3DKMDT\_プリエンプション\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_SUBMITCOMMANDFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)
-   [**DXGKARGCB\_CREATECONTEXTALLOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_createcontextallocation)

## <a name="span-iddisplay_miniport_driver_implementationspanspan-iddisplay_miniport_driver_implementationspanspan-iddisplay_miniport_driver_implementationspandisplay-miniport-driver-implementation"></a><span id="Display_miniport_driver_implementation"></span><span id="display_miniport_driver_implementation"></span><span id="DISPLAY_MINIPORT_DRIVER_IMPLEMENTATION"></span>ミニポートドライバーの実装を表示する


ディスプレイミニポートドライバーに Windows 8 GPU プリエンプションモデルを実装するには、次の一般的な手順に従います。

1.  **Dxgkddi\_interface\_version** &gt;= **DXGKDDI\_interface\_version\_WIN8**を持つヘッダーに対してドライバーをコンパイルします。
2.  [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)構造体の**PreemptionAware**メンバーと**MultiEngineAware**メンバーを1に設定して、Windows 8 GPU プリエンプションモデルのサポートを宣言します。 Windows 7 のプリエンプションモデルをサポートするには、 **PreemptionAware**を0に設定します。
3.  [**D3DKMDT\_プリエンプション\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps)構造体でサポートされている優先権レベルを指定します。これは、D3DKMDT\_グラフィックスから定数値を取得し[ **\_プリエンプション\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity) [**D3DKMDT\_\_プリエンプション\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity)列挙体を計算します。
4.  ハードウェアが遅延コンテキストの切り替えをサポートしている場合は、長さ0のバッファーを[*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数に送信し、 *psubmitcommand*-&gt;**Flags**-&gt;**contextswitch**メンバーを1に設定します。 [**DXGK\_SUBMITCOMMANDFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)構造体の**contextswitch**メンバーの説明に注意してください。
5.  [*DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)関数を呼び出して、GPU コンテキストの割り当てとデバイスコンテキストの割り当てを設定します。 関数の解説に記載されている具体的な指示と制限に注意してください。
6.  [*Dxgkcbdestroycontextallocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation)関数を呼び出して、 [*DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)で作成された GPU コンテキストの割り当てとデバイスコンテキストの割り当てを破棄します。
7.  [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数の呼び出しに応答して DMA バッファーを準備するときに、 [**Dxgkarg\_BUILDPAGINGBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)構造体内に**initcontextresource**内部構造体を入力して、コンテキストリソースを初期化します。 コンテキストリソースが削除または再配置されると、ビデオメモリマネージャーによってコンテキストリソースの内容が保持されます。
8.  ドライバーは、次の垂直方向の同期で、メモリマップト i/o フリップをサポートする必要があります。Windows 8 では、フリップが保留中の場合でも、GPU スケジューラはハードウェアのプリエンプトを試行します。 そのため、分裂とレンダリングのアーティファクトを防ぐには、ドライバーがメモリマップト i/o フリップモデルをサポートしている必要があります。また、 [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)構造体の**FlipOnVSyncMmIo**メンバーを1に設定し、「」で説明されている操作をサポートする必要があります。**FlipOnVSyncMmIo**。

### <a name="span-idmemory_mapping_considerations_in_your_implementationspanspan-idmemory_mapping_considerations_in_your_implementationspanspan-idmemory_mapping_considerations_in_your_implementationspanmemory-mapping-considerations-in-your-implementation"></a><span id="Memory_mapping_considerations_in_your_implementation"></span><span id="memory_mapping_considerations_in_your_implementation"></span><span id="MEMORY_MAPPING_CONSIDERATIONS_IN_YOUR_IMPLEMENTATION"></span>実装におけるメモリマッピングに関する考慮事項

Windows 8 GPU プリエンプションモデルをサポートする堅牢なドライバーを作成し、次のガイダンスに従って品質の高いユーザーエクスペリエンスを提供します。

-   DirectX グラフィックスカーネル (Dxgkrnl) スケジューラがプリエンプションコマンドを送信するときに、GPU から DMA バッファープリエンプションを要求します。 DMA バッファープリエンプションの粒度が細かいハードウェアデバイスでは、より優れたカスタマーエクスペリエンスが得られます。
-   ページングコマンドフェンス Id を再利用できるようにする: プリエンプション要求によってハードウェアキュー内のインメモリコマンドが先取りされた場合、Dxgkrnl scheduler は、最初に使用されたものと同じフェンス Id を使用して割り込まれたページングコマンドを再送信し、ページングを行います。コマンドは、そのエンジンの他のコマンドの前にスケジュールされます。 ページング以外のコマンドは、新たに割り当てられたフェンス Id で再送信されます。
-   分割した DMA バッファーのパッチの場所の一覧を指定します。「 [Dma バッファーの分割](splitting-a-dma-buffer.md)」を参照してください。
-   バインドリーク検出と呼ばれる検証モードを利用できます。このモードでは、パッチの場所の一覧を参照し、バインド解除されていないパケットを拒否します。または、分割された各パケットの割り当てを更新しません。 一部のハードウェアでは仮想アドレスがサポートされているため、この検証を不要にする追加のレベルの間接参照が可能になります。 このような場合、ドライバーが検証モードを終了することを示すには、 [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)構造体の**NoDmaPatching**メンバーを1に設定します。
-   Windows 7 では、Dxgkrnl scheduler は、同じ render コマンドに対応するすべての分割された DMA パケットが、別のレンダリングコンテキストに切り替えずに順番に実行されることを保証します。 Windows 8 のプリエンプションモデルでは、scheduler は、同じ render コマンドに対応する2つの分割パケット間で異なるコンテキストからレンダーパケットを実行できます。 その結果、プリエンプションを認識しているドライバーは、通常の完全なパケット送信と同じ方法で、分割または部分的な DMA パケットの送信を処理する必要があります。 特に、GPU 状態は、このような送信のために境界で保存または復元する必要があります。
-   複数の物理 Gpu がリンクされた1つの高速な仮想 GPU を形成するためにリンクされている場合、LDA (リンクされたディスプレイアダプター) モードで複数のアダプターにブロードキャストするときに、プリエンプション対応ドライバーは分割された DMA バッファーの内容を変更しないようにする必要があります。 これは、Windows 8 のプリエンプションモデルでは、Dxgkrnl scheduler によって、別のコンテキストに切り替えずに、分割パケットシーケンスの同期実行が保証されなくなったためです。 分離された DMA パケットの内容を変更したドライバーは、パケットが別のエンジンで実行された場合、同じコピーの DMA バッファーデータで動作するため、パケットのデータの整合性を損なう可能性があります。
-   Windows 8 GPU プリエンプションモデルでは、Dxgkrnl scheduler によって "signal on submit" 同期プリミティブが関連付けられているパケットのプリエンプションが有効になります。 デバイスがハードウェアベースの待機状態と共に "送信時に通知" 同期プリミティブを使用する場合、待機条件が満たされる前に待機命令を切断する機能をサポートする必要があります。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細[について](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)は、**デバイス...プリエンプションテスト**と**デバイス...FlipOnVSyncMmIo**。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





