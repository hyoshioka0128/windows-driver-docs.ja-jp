---
title: WDDM 1.2 の機能
description: このトピックでは、パフォーマンス、信頼性、および全体的なエンド ユーザー エクスペリエンスを向上させるいくつかの新しい拡張機能を含む Windows Display Driver Model (WDDM) Version 1.2 の機能セットについて説明します。
ms.assetid: 65072545-76F0-43A8-9E46-703CA99BFE90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff70e630d512cb1581008534d8757ae0020eda5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353407"
---
# <a name="wddm-12-features"></a>WDDM 1.2 の機能


このトピックでは、パフォーマンス、信頼性、および全体的なエンド ユーザー エクスペリエンスを向上させるいくつかの新しい拡張機能を含む Windows Display Driver Model (WDDM) Version 1.2 の機能セットについて説明します。

これらの各機能には、サード パーティ製 WDDM 1.2 およびそれ以降のドライバーからの特別なサポートが必要です。 このセクションでは、WDDM 1.2 の機能セットの構成内容について詳しく説明します。

WDDM 1.2 には、必須およびオプションの両方の機能があります。 ドライバーとして自体を要求するすべての必須機能を実装する必要があります、"WDDM 1.2 ドライバー"オプションの機能の任意の組み合わせ (または none) ドライバーを実装できます。 非-WDDM 1.2 ドライバーには、WDDM 1.2 機能はありませんを報告する必要があります。

このテーブルは、WDDM 1.2 の機能セットをまとめたものです。 "M"必須ですが、"O"が、省略可能なことを示します示し"NA"該当なし。 各機能の詳細を読み取り、左の列で、リンクをクリックします。

**WDDM 1.2 機能セット**

| Windows 8 の機能および WDDM 1.2 を有効になっています。                                                                         | 機能の利点                                                                                                            | WDDM ドライバーの種類:完全なグラフィック | WDDM ドライバーの種類:表示のみ | WDDM ドライバーの種類:のみを表示します。 |
|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------------------|-------------------------------|--------------------------------|
| [ビデオ メモリのプランと再利用](video-memory-offer-and-reclaim.md)                                           | ビデオ メモリの使用状況をより効率的な有効にします。                                                                               | M                               | M                             | 該当なし                             |
| [GPU のプリエンプション](gpu-preemption.md)                                                                           | デスクトップの応答性を向上します。                                                                                            | M                               | M                             | 該当なし                             |
| [Windows 8 での TDR の変更](tdr-changes-in-windows-8.md)                                                       | GPU がハングする堅牢性の向上                                                                                           | M                               | M                             | 該当なし                             |
| [最適化された画面の回転のサポート](optimized-screen-rotation-support.md)                                     | ちらつきなしの画面の回転のエクスペリエンス                                                                                 | M                               | 該当なし                            | M                              |
| [ステレオスコ ピック 3D](stereoscopic-3d.md)                                                                         | ステレオスコ ピック 3D シナリオを有効にする一貫性のある API と DDI プラットフォームを提供します                                             | O                               | 該当なし                            | 該当なし                             |
| [Direct3d11 のビデオ再生の機能強化](d3d11-video-playback-improvements.md)                               | ビデオの再生アプリケーションのプログラミング エクスペリエンスを簡略化されました。                                                          | M\*                             | M\*                           | 該当なし                             |
| [ビデオ メモリの直接の反転](direct-flip-of-video-memory.md)                                                 | 電力消費量を削減するビデオの再生およびコンポジション スタック内の機能強化                                       | M                               | 該当なし                            | 該当なし                             |
| [シームレスな状態遷移を提供します。](seamless-state-transitions-in-wddm-1-2-and-later.md)                   | 状態遷移ではバグの確認中に、高解像度が保持されます。                                                   | M                               | 該当なし                            | M                              |
| [プラグ アンド プレイ (PnP) の開始と停止](plug-and-play--pnp--start-and-stop-cases.md)                             | 表示の所有権は、ファームウェア、Windows、およびドライバーの間で切り替えが高解像度を維持します。                        | M                               | 該当なし                            | M                              |
| [スタンバイの最適化を休止状態します。](standby-hibernate-optimizations.md)                                         | グラフィックス スタックにスリープ状態でパフォーマンスが向上し、再開の最適化を有効にします。                                     | O                               | O                             | 該当なし                             |
| [アイドル状態とアクティブな電源の GPU の電源管理](gpu-power-management-of-idle-and-active-power.md)      | 詳細なデバイスの電源管理の標準化されたインフラストラクチャを提供します。                                            | O                               | O                             | O                              |
| [GPU 上で XPS ラスタライズ](xps-rasterization-on-the-gpu.md)                                               | により、サードパーティ製のドライバーを Windows で高品質な印刷エクスペリエンス                                                  | M\*\*                           | M\*\*                         | 該当なし                             |
| [表示でコンテナー ID のサポート](container-id-support-for-displays-.md)                                    | により、デバイスのハブに似たユーザー インターフェイスでユーザーにデバイスの接続性の監視と関連付けられた状態を表す | M                               | 該当なし                            | M                              |
| [フレーム ポインターの省略 (FPO) の最適化を無効にします。](disabling-frame-pointer-omission--fpo--optimization.md) | FPO フィールドに関連するパフォーマンスの問題のデバッグが向上します。                                                     | M                               | M                             | M                              |
| [ユーザー モード ドライバーのログ記録](user-mode-driver-logging.md)                                                       | 診断し、メモリの使用状況を分かりやすく表示を提供することによってメモリ関連の問題を調査する機能が向上します。              | M                               | M                             | 該当なし                             |

 

\*この機能は、すべての WDDM 1.2 ドライバーと Microsoft Direct3D 10 で、必須 10.1、11、または 11.1 対応ハードウェア (またはそれ以降)。

\*\*新しいデバイス ドライバー インターフェイス (DDI) または動作の変更はありません。 ただし、WDDM 1.2 およびそれ以降のドライバーは XPS 印刷シナリオのハードウェア アクセラレータを使用した高品質な印刷エクスペリエンスを確実にラスタライズ準拠テストを XML Paper Specification (XPS) を渡すことがある必要があります。

**注**  一連の Api は、コラボレーションのシナリオ用のデスクトップを複製するための Windows 8 以降から使用できます。 詳細については、次を参照してください。[デスクトップ重複](desktop-duplication-api.md)します。

 

## <a name="span-idadditionalnewfeaturesinwindows8spanspan-idadditionalnewfeaturesinwindows8spanspan-idadditionalnewfeaturesinwindows8spanadditional-new-features-in-windows8"></a><span id="Additional_new_features_in_Windows_8"></span><span id="additional_new_features_in_windows_8"></span><span id="ADDITIONAL_NEW_FEATURES_IN_WINDOWS_8"></span>Windows 8 の新機能の追加


次の新しいまたは更新された表示ドライバー Ddi は、Windows 8 で提供されるも示します。

[**カーネル モードの表示専用ドライバー (KMDOD) インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

限られた表示機能のない表示機能を提供します。

**注**  にも参照してください、[カーネル モードの表示専用のミニポート ドライバー](https://go.microsoft.com/fwlink/p/?linkid=258742)サンプル。

 

[**SPB インターフェイスを通じてチップ (SoC) アーキテクチャ上のシステムのサポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

SoC のシステムで表示ミニポート ドライバー アクセス bus リソースをことができます。

### <a name="span-idsurpriseremovalofsecondaryadapterspanspan-idsurpriseremovalofsecondaryadapterspanspan-idsurpriseremovalofsecondaryadapterspansurprise-removal-of-secondary-adapter"></a><span id="Surprise_removal_of_secondary_adapter"></span><span id="surprise_removal_of_secondary_adapter"></span><span id="SURPRISE_REMOVAL_OF_SECONDARY_ADAPTER"></span>セカンダリのアダプターの突然の取り外し

-   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal)
-   [**DXGK\_SURPRISE\_REMOVAL\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_surprise_removal_type)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**D3DKMT\_WDDM\_1\_2\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/display/d3dkmt-wddm-1-2-caps)

[**システム ファームウェア テーブル インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_firmware_table_interface)

表示のミニポート ドライバーを列挙し、システム ファームウェアのテーブルを読み取ることができます。

[**明るさコントロール インターフェイス V です。2 (適応型かつスムーズな明るさコントロール)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

表示のバックライトのパワーし、スムーズに依然周辺光と明るさを変更するユーザーの要求の変化に適応表示ミニポート ドライバーを使用できます。

参照してください[統合ディスプレイの明るさコントロールを Windows 8](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614018(v=vs.85))します。

### <a name="span-idmicrosoftdirectxgraphicsinfrastructureddidxgispanspan-idmicrosoftdirectxgraphicsinfrastructureddidxgispanspan-idmicrosoftdirectxgraphicsinfrastructureddidxgispanmicrosoft-directx-graphics-infrastructure-ddi-dxgi"></a><span id="Microsoft_DirectX_Graphics_Infrastructure_DDI__DXGI_"></span><span id="microsoft_directx_graphics_infrastructure_ddi__dxgi_"></span><span id="MICROSOFT_DIRECTX_GRAPHICS_INFRASTRUCTURE_DDI__DXGI_"></span>Microsoft DirectX のグラフィックス インフラストラクチャ DDI (DXGI)

-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [**DXGI\_DDI\_ARG\_BLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt1)
-   [**DXGI\_DDI\_ベース\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)
-   [**DXGI1\_2\_DDI\_ベース\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

### <a name="span-idallocationsharingenqueinggpueventsspanspan-idallocationsharingenqueinggpueventsspanspan-idallocationsharingenqueinggpueventsspanallocation-sharing--enqueing-gpu-events"></a><span id="Allocation_sharing___enqueing_GPU_events"></span><span id="allocation_sharing___enqueing_gpu_events"></span><span id="ALLOCATION_SHARING___ENQUEING_GPU_EVENTS"></span>割り当ての共有と enqueing GPU イベント

-   [*pfnCreateSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobject2cb)
-   [*pfnSignalSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobject2cb)
-   [*pfnWaitForSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobject2cb)
-   [**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DDDICB\_CREATESYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_createsynchronizationobject2)
-   [**D3DDDICB\_SIGNALFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_signalflags)
-   [**D3DDDICB\_SIGNALSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_signalsynchronizationobject2)
-   [**D3DDDICB\_WAITFORSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_waitforsynchronizationobject2)
-   [**D3DKMT\_CREATEALLOCATIONFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createallocationflags)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2_flags)
-   [**D3DKMT\_RELEASEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_releasekeyedmutex2)
-   [**D3DKMTShareObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtshareobjects)

### <a name="span-idcancelcommandinterfacespanspan-idcancelcommandinterfacespanspan-idcancelcommandinterfacespancancel-command-interface"></a><span id="Cancel_command_interface"></span><span id="cancel_command_interface"></span><span id="CANCEL_COMMAND_INTERFACE"></span>Cancel コマンド インターフェイス

-   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand)
-   [**DXGKARG\_CANCELCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_cancelcommand)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)

### <a name="span-idoutputduplicationspanspan-idoutputduplicationspanspan-idoutputduplicationspanoutput-duplication"></a><span id="Output_duplication"></span><span id="output_duplication"></span><span id="OUTPUT_DUPLICATION"></span>出力の重複

-   [**D3DKMTOutputDuplPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplpresent)
-   [**D3DKMTOutputDuplReleaseFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplreleaseframe)
-   [**D3DKMT\_OUTPUTDUPL\_リリース\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_release_frame)
-   [**D3DKMT\_OUTPUTDUPL\_スナップショット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_snapshot)
-   [**D3DKMT\_OUTPUTDUPLCONTEXTSCOUNT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplcontextscount)
-   [**D3DKMT\_OUTPUTDUPLPRESENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresent)
-   [**D3DKMT\_OUTPUTDUPLPRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresentflags)
-   [**D3DKMT\_存在\_RGNS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_present_rgns)

[**Windows 8 の OpenGL の機能強化**](supporting-opengl-enhancements.md)

OpenGL インストール可能なクライアント ドライバー (ICDs) は、リソースへのアクセスを制御し、オブジェクトと id の間にマップする新しい関数を呼び出すことができます。

 

 





