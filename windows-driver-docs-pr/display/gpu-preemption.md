---
title: GPU プリエンプション
description: 新しい GPU 優先権モデルでは、Windows 8 以降で使用できます。
ms.assetid: 9382786E-2E1E-408F-A9E9-04EEEA1CC34A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9a82d289cf09ab3eddea7d73813308d82b1721
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379474"
---
# <a name="gpu-preemption"></a>GPU プリエンプション


新しい GPU 優先権モデルでは、Windows 8 以降で使用できます。 このモデルではオペレーティング システムされなく GPU ダイレクト メモリの優先を無効にする、アクセス (DMA) パケットでは、割り込み要求する前に、GPU に送信されることが保証されます、[タイムアウト検出と復旧 (TDR)](timeout-detection-and-recovery.md)プロセスが開始されます。

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
<td align="left">ドライバーの実装: 完全なグラフィックスとレンダリングのみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics.プリエンプションのテスト</strong></p>
<p><strong>Device.Graphics.FlipOnVSyncMmIo</strong></p></td>
</tr>
</tbody>
</table>

 

長時間実行されるパケットが正常に割り込まれることはできません、デスクトップ ウィンドウ マネージャー (DWM) によって必要な作業などの優先度の高い GPU 作業が遅れて、ウィンドウの切り替えやアニメーションの中にエラーになります。 また、TDR プロセスを繰り返し、GPU をリセットする可能性が割り込まれることはできません、実行時間の長い GPU パケット、システムでバグチェックを最終的に発生することができます。

**注**   WDDM 1.2 がすべて表示ミニポート ドライバーが Windows 8 優先権モデルをサポートする必要があります。 ただし、操作の場合および WDDM 1.2 ドライバーも Windows 8 のプリエンプション モデルを拒否でき Microsoft DirectX グラフィックスのカーネル サブシステム スケジューラによって、Windows 7 の動作を維持できます。

 

## <a name="span-idgpupreemptiondevicedriverinterfacesddisspanspan-idgpupreemptiondevicedriverinterfacesddisspanspan-idgpupreemptiondevicedriverinterfacesddisspangpu-preemption-device-driver-interfaces-ddis"></a><span id="GPU_preemption_device_driver_interfaces__DDIs_"></span><span id="gpu_preemption_device_driver_interfaces__ddis_"></span><span id="GPU_PREEMPTION_DEVICE_DRIVER_INTERFACES__DDIS_"></span>GPU 優先権デバイス ドライバー インターフェイス (Ddi)


次のデバイス ドライバー インターフェイス (Ddi)、Windows 8 の GPU 優先権モデルを実装するためにディスプレイのミニポート ドライバーを利用できます。

-   [*DxgkCbCreateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/hh451312)
-   [*DxgkCbDestroyContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/hh451317)
-   [*pfnSetPriorityCb*](https://msdn.microsoft.com/library/windows/hardware/ff568931)
-   [Dxgkrnl インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff560940)
-   [**DXGKRNL\_INTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff560942)
-   [**D3DKMDT\_コンピューティング\_優先権\_粒度**](https://msdn.microsoft.com/library/windows/hardware/hh439326)
-   [**D3DKMDT\_グラフィックス\_優先権\_粒度**](https://msdn.microsoft.com/library/windows/hardware/hh439329)
-   [**D3DKMDT\_優先権\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh439334)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://msdn.microsoft.com/library/windows/hardware/ff548203)
-   [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)
-   [**DXGK\_SUBMITCOMMANDFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562058)
-   [**DXGK\_VIDSCHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562863)
-   [**DXGKARGCB\_CREATECONTEXTALLOCATION**](https://msdn.microsoft.com/library/windows/hardware/hh451242)

## <a name="span-iddisplayminiportdriverimplementationspanspan-iddisplayminiportdriverimplementationspanspan-iddisplayminiportdriverimplementationspandisplay-miniport-driver-implementation"></a><span id="Display_miniport_driver_implementation"></span><span id="display_miniport_driver_implementation"></span><span id="DISPLAY_MINIPORT_DRIVER_IMPLEMENTATION"></span>ミニポート ドライバーの実装を表示します。


ディスプレイ ミニポート ドライバーでは、Windows 8 の GPU 優先権モデルを実装する一般的な手順に従います。

1.  コンパイル、ドライバーを持つヘッダーに対して**DXGKDDI\_インターフェイス\_バージョン** &gt; =  **DXGKDDI\_インターフェイス\_バージョン\_WIN8**します。
2.  設定して、Windows 8 の GPU 優先権モデルのサポートを宣言、 **PreemptionAware**と**MultiEngineAware**のメンバー、 [ **DXGK\_VIDSCHCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff562863)構造体を 1 にします。 Windows 7 の優先モデルをサポートするために次のように設定します。 **PreemptionAware**をゼロにします。
3.  プリエンプションの粒度でのサポートされているレベルを指定、 [ **D3DKMDT\_優先権\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/hh439334)構造体、定数値を取ります、 [ **D3DKMDT\_グラフィックス\_優先権\_粒度**](https://msdn.microsoft.com/library/windows/hardware/hh439329)と[ **D3DKMDT\_コンピューティング\_優先権\_粒度**](https://msdn.microsoft.com/library/windows/hardware/hh439326)列挙体。
4.  ハードウェアでは、遅延のコンテキストの切り替えをサポートする場合に長さ 0 のバッファーを送信、 [ *DxgkDdiSubmitCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff560790)機能、設定、 *pSubmitCommand* - &gt;**フラグ**-&gt;**ContextSwitch**メンバーを 1 にします。 」の説明に注意してください、 **ContextSwitch**のメンバー、 [ **DXGK\_SUBMITCOMMANDFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562058)構造体。
5.  GPU コンテキスト、デバイス コンテキストの割り当てを呼び出すことによって設定、 [ *DxgkCbCreateContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/hh451312)関数。 具体的な手順と、関数の「解説」で指定された制限に注意してください。
6.  呼び出す、 [ *DxgkCbDestroyContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/hh451317) GPU コンテキストで作成されたデバイス コンテキストの割り当てを破棄[ *DxgkCbCreateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/hh451312)します。
7.  DMA バッファーへの呼び出しに応答を準備するときに、 [ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)関数を入力することで、コンテキストのリソースを初期化、 **InitContextResource**内での内部構造、 [ **DXGKARG\_BUILDPAGINGBUFFER** ](https://msdn.microsoft.com/library/windows/hardware/ff557540)構造体。 コンテキストのリソースは削除または再配置は、ビデオ メモリ マネージャーのコンテキストのリソースのコンテンツが保持されます。
8.  ドライバーは、[次へ] の垂直方向の同期時にメモリ マップ I/O フリップをサポートする必要があります。Windows 8、GPU のスケジューラは反転が保留になっている場合でも、ハードウェアを切断しようとします。 そのため、ティアリングとの成果物をレンダリングを防ぐため、ドライバー、メモリ マップ I/O のフリップ モデルをサポートする必要があり、設定する必要があります、 **FlipOnVSyncMmIo**のメンバー、 [ **DXGK\_FLIPCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561069)構造体を 1 とで説明されている操作をサポートして**FlipOnVSyncMmIo**します。

### <a name="span-idmemorymappingconsiderationsinyourimplementationspanspan-idmemorymappingconsiderationsinyourimplementationspanspan-idmemorymappingconsiderationsinyourimplementationspanmemory-mapping-considerations-in-your-implementation"></a><span id="Memory_mapping_considerations_in_your_implementation"></span><span id="memory_mapping_considerations_in_your_implementation"></span><span id="MEMORY_MAPPING_CONSIDERATIONS_IN_YOUR_IMPLEMENTATION"></span>実装でメモリ マッピングに関する注意点

Windows 8 の GPU 優先権モデルをサポートし、このガイダンスに従って、高品質なユーザー エクスペリエンスを提供する堅牢なドライバーを作成します。

-   DirectX グラフィックスのカーネル (Dxgkrnl) スケジューラが優先コマンドを送信する GPU から DMA mid バッファー優先権を要求します。 DMA mid バッファー プリエンプションの粒度の細かいのあるハードウェア デバイスでは、カスタマー エクスペリエンスの向上を生成する必要があります。
-   コマンドのフェンスを再利用の Id のページングを許可する: スケジューラが再送信 Dxgkrnl に同じフェンス、およびページングに使用された元の Id とページング コマンドが割り込まれたハードウェア キューでページング コマンドの優先が発生した割り込み要求場合、コマンドは、そのエンジンの他のコマンドの前にスケジュールされます。 新しく割り当てられたフェンス Id では、非ページング コマンドを再送信されます。
-   分割 DMA バッファーの修正プログラムの場所の一覧を提供するを参照してください[DMA バッファーを分割](splitting-a-dma-buffer.md)します。
-   バインド リークの検出と呼ばれる、認証モードが使用できるは、更新プログラムの場所を見ていきますが一覧表示し、パケットをアンバインドしないまたはを各パケットの分割の割り当てを再設定されませんを拒否します。 一部のハードウェアは、この検証が不要の間接参照の追加のレベルを許可、仮想のアドレスをサポートします。 このような場合は、ドライバーがオプトアウト検証モードを示す、設定、 **NoDmaPatching**のメンバー、 [ **DXGK\_VIDSCHCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff562863)構造体を 1 にします。
-   Windows 7 を別のレンダリング コンテキストを切り替えずに順番にスケジューラと同じに対応するすべての分割 DMA パケットがコマンドを表示することを保証 Dxgkrnl が実行されます。 モデルでは、Windows 8 優先、スケジューラは同じレンダリング コマンドに対応する 2 つの分割パケットの間、別のコンテキストからレンダリング パケットを実行できます。 その結果は優先権を意識してドライバーを正規の完全なパケットの送信と同じ方法で分割と部分的な DMA パケットの送信を処理します。 具体的には、GPU の状態を保存または、このような送信の境界で復元される必要があります。
-   プリエンプション対応ドライバー仮想 GPU を高速化、1 つを形成する複数の物理 Gpu をリンク先をリンクの表示アダプター (LDA) モードで複数のアダプターにブロードキャストされる分割の DMA バッファーの内容は変更されませんする必要があります。 これは、モデルでは、Windows 8 優先、Dxgkrnl スケジューラ不要になったことを保証分割パケットの順序の同期の実行を別のコンテキストを切り替えずにためにです。 分割 DMA パケットの内容が変更されたドライバーには、パケットが別のエンジンで実行された場合と同じ DMA バッファー データのコピーの動作はためパケットのデータの整合性が損なわれます。
-   Windows 8 の GPU 優先権モデルでは、Dxgkrnl スケジューラは、「信号を送信」の同期プリミティブに関連付けられているパケットの優先を使用できます。 デバイスで使用する場合は、ハードウェア ベースと組み合わせて「信号を送信」の同期プリミティブの待機状態、待機条件が満たされる前に待機命令を切断する機能をサポートする必要があります。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.プリエンプション テスト**と**Device.Graphics.FlipOnVSyncMmIo**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





