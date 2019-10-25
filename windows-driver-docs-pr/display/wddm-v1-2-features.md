---
title: WDDM 1.2 の機能
description: このトピックでは、Windows Display Driver Model (WDDM) バージョン1.2 の機能セットについて説明します。この機能セットには、パフォーマンス、信頼性、およびエンドユーザーエクスペリエンス全体を向上させるいくつかの新しい機能強化が含まれています。
ms.assetid: 65072545-76F0-43A8-9E46-703CA99BFE90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e49e1b0ef745ba83689778755a7c6ee3fef354c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829177"
---
# <a name="wddm-12-features"></a>WDDM 1.2 の機能


このトピックでは、Windows Display Driver Model (WDDM) バージョン1.2 の機能セットについて説明します。この機能セットには、パフォーマンス、信頼性、およびエンドユーザーエクスペリエンス全体を向上させるいくつかの新しい機能強化が含まれています。

これらの各機能には、サードパーティ製の WDDM 1.2 以降のドライバーからの特別なサポートが必要です。 このセクションでは、WDDM 1.2 機能セットの構成要素について詳述します。

WDDM 1.2 には、必須の機能とオプションの機能の両方があります。 ドライバーは、"WDDM 1.2 ドライバー" として要求するすべての必須機能を実装する必要があります。一方、ドライバーはオプション機能の任意の組み合わせを実装できます。 WDDM 以外の1.2 ドライバーは、WDDM 1.2 の機能を一切報告する必要はありません。

次の表は、WDDM 1.2 機能セットをまとめたものです。 "M" は必須であり、"O" は省略可能であることを示し、"NA" は適用されないことを示します。 各機能の詳細を確認するには、左側の列にあるリンクを参照してください。

**WDDM 1.2 機能セット**

| WDDM 1.2 で有効になっている Windows 8 の機能                                                                         | 機能の特典                                                                                                            | WDDM ドライバーの種類: 完全なグラフィックス | WDDM ドライバーの種類: レンダーのみ | WDDM ドライバーの種類: 表示のみ |
|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------------------|-------------------------------|--------------------------------|
| [ビデオメモリの提供と回収](video-memory-offer-and-reclaim.md)                                           | ビデオメモリの効率的な使用を可能にします                                                                               | [M]                               | [M]                             | 該当なし                             |
| [GPU プリエンプション](gpu-preemption.md)                                                                           | デスクトップの応答性を向上させる                                                                                            | [M]                               | [M]                             | 該当なし                             |
| [Windows 8 での TDR の変更点](tdr-changes-in-windows-8.md)                                                       | GPU ハングの回復性の向上                                                                                           | [M]                               | [M]                             | 該当なし                             |
| [最適化された画面ローテーションのサポート](optimized-screen-rotation-support.md)                                     | 画面の回転エクスペリエンス (ちらつきなし)                                                                                 | [M]                               | 該当なし                            | [M]                              |
| [ステレオスコピック3D](stereoscopic-3d.md)                                                                         | ステレオスコピック3D シナリオを実現するための一貫した API と DDI プラットフォームを提供します                                             | O                               | 該当なし                            | 該当なし                             |
| [Direct3D 11 ビデオ再生の機能強化](d3d11-video-playback-improvements.md)                               | ビデオ再生アプリケーションのプログラミングエクスペリエンスが簡略化されました                                                          | M @ no__t_0_                             | M @ no__t_0_                           | 該当なし                             |
| [ビデオメモリの直接フリップ](direct-flip-of-video-memory.md)                                                 | 電力消費を削減するためのビデオ再生とコンポジションスタックの機能強化                                       | [M]                               | 該当なし                            | 該当なし                             |
| [シームレスな状態遷移の提供](seamless-state-transitions-in-wddm-1-2-and-later.md)                   | 高解像度は状態遷移、バグチェック中に保持されます。                                                   | [M]                               | 該当なし                            | [M]                              |
| [プラグアンドプレイ (PnP) の開始と停止](plug-and-play--pnp--start-and-stop-cases.md)                             | ディスプレイの所有権がファームウェア、Windows、ドライバーの間で移行されるため、高解像度を維持する                        | [M]                               | 該当なし                            | [M]                              |
| [スタンバイ休止状態の最適化](standby-hibernate-optimizations.md)                                         | スリープと再開のパフォーマンスを向上させるために、グラフィックススタックへの最適化を有効にします。                                     | O                               | O                             | 該当なし                             |
| [アイドル状態とアクティブな電源の GPU 電源管理](gpu-power-management-of-idle-and-active-power.md)      | きめ細かなデバイス電源管理のための標準化されたインフラストラクチャを提供します。                                            | O                               | O                             | O                              |
| [GPU での XPS ラスタライズ](xps-rasterization-on-the-gpu.md)                                               | サードパーティ製のドライバーを使用して Windows で品質の印刷エクスペリエンスを有効にします。                                                  | M @ no__t_0_\*                           | M @ no__t_0_\*                         | 該当なし                             |
| [コンテナー ID による表示のサポート](container-id-support-for-displays-.md)                                    | デバイスハブと同様のユーザーインターフェイスで、デバイスの接続と関連付けられた状態をユーザーに示すことができます。 | [M]                               | 該当なし                            | [M]                              |
| [フレームポインターの省略 (FPO) の最適化を無効にする](disabling-frame-pointer-omission--fpo--optimization.md) | フィールドの FPO に関連するパフォーマンスの問題のデバッグ機能を強化します。                                                     | [M]                               | [M]                             | [M]                              |
| [ユーザーモードドライバーのログ記録](user-mode-driver-logging.md)                                                       | メモリ使用量の表示を向上させることで、メモリ関連の問題を診断および調査する機能を向上させます。              | [M]                               | [M]                             | 該当なし                             |

 

\*この機能は、Microsoft Direct3D 10-、10.1-、11または11.1 対応のハードウェア (またはそれ以降) を搭載したすべての WDDM 1.2 ドライバーに必須です。

\*\*新しいデバイスドライバーインターフェイス (DDI) や動作の変更はありません。 ただし、WDDM 1.2 以降のドライバーは、ハードウェアアクセラレータの XPS 印刷シナリオで品質の印刷を実現するために、XML Paper Specification (XPS) ラスタライズの適合性テストを渡すことができる必要があります。

Windows 8 以降では、コラボレーションのシナリオでデスクトップを複製するために、新しい Api のセットを使用できる   に**注意**してください。 詳細については、「[デスクトップの複製](desktop-duplication-api.md)」を参照してください。

 

## <a name="span-idadditional_new_features_in_windows_8spanspan-idadditional_new_features_in_windows_8spanspan-idadditional_new_features_in_windows_8spanadditional-new-features-in-windows8"></a><span id="Additional_new_features_in_Windows_8"></span><span id="additional_new_features_in_windows_8"></span><span id="ADDITIONAL_NEW_FEATURES_IN_WINDOWS_8"></span>Windows 8 のその他の新機能


Windows 8 では、次の新しいまたは更新されたディスプレイドライバー DDIs も提供されています。

[**カーネルモード表示専用ドライバー (KMDOD) インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

表示機能を持たない、限られた表示関数のセットを提供します。

**注**  [カーネルモードの表示専用ミニポートドライバー](https://go.microsoft.com/fwlink/p/?linkid=258742)のサンプルも参照してください。

 

[**SPB インターフェイスを使用したチップ (SoC) アーキテクチャでのシステムのサポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

アドオンのミニポートドライバーが SoC システム上のバスリソースにアクセスできるようにします。

### <a name="span-idsurprise_removal_of_secondary_adapterspanspan-idsurprise_removal_of_secondary_adapterspanspan-idsurprise_removal_of_secondary_adapterspansurprise-removal-of-secondary-adapter"></a><span id="Surprise_removal_of_secondary_adapter"></span><span id="surprise_removal_of_secondary_adapter"></span><span id="SURPRISE_REMOVAL_OF_SECONDARY_ADAPTER"></span>セカンダリアダプターの突然の削除

-   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal)
-   [**DXGK\_突然\_削除\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_surprise_removal_type)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**D3DKMT\_WDDM\_1\_2\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/display/d3dkmt-wddm-1-2-caps)

[**システムファームウェアテーブルインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_firmware_table_interface)

[ミニポートドライバーの表示] を使用すると、システムファームウェアテーブルを列挙して読み取ることができます。

[**輝度コントロールインターフェイス v. 2 (アダプティブおよび Smooth 輝度コントロール)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

ミニポートドライバーの表示を使用すると、ディスプレイのバックライトに電力を抑えることができます。また、アンビエントライトとユーザー要求の変化にスムーズに適応し、明るさを変更できます。

[統合ディスプレイについては、「Windows 8 の輝度コントロール](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614018(v=vs.85))」も参照してください。

### <a name="span-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanspan-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanspan-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanmicrosoft-directx-graphics-infrastructure-ddi-dxgi"></a><span id="Microsoft_DirectX_Graphics_Infrastructure_DDI__DXGI_"></span><span id="microsoft_directx_graphics_infrastructure_ddi__dxgi_"></span><span id="MICROSOFT_DIRECTX_GRAPHICS_INFRASTRUCTURE_DDI__DXGI_"></span>Microsoft DirectX グラフィックスインフラストラクチャ DDI (DXGI)

-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [**DXGI\_DDI\_ARG\_BLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt1)
-   [**DXGI\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)
-   [**DXGI1\_2\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

### <a name="span-idallocation_sharing___enqueing_gpu_eventsspanspan-idallocation_sharing___enqueing_gpu_eventsspanspan-idallocation_sharing___enqueing_gpu_eventsspanallocation-sharing--enqueing-gpu-events"></a><span id="Allocation_sharing___enqueing_GPU_events"></span><span id="allocation_sharing___enqueing_gpu_events"></span><span id="ALLOCATION_SHARING___ENQUEING_GPU_EVENTS"></span>Enqueing GPU イベント & の割り当て共有

-   [*pfnCreateSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobject2cb)
-   [*pfnSignalSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobject2cb)
-   [*pfnWaitForSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobject2cb)
-   [**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)
-   [**D3DDDI\_同期オブジェクト\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DDDICB\_CREATESYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createsynchronizationobject2)
-   [**D3DDDICB\_SIGNALFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_signalflags)
-   [**D3DDDICB\_SIGNALSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_signalsynchronizationobject2)
-   [**D3DDDICB\_WAITFORSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_waitforsynchronizationobject2)
-   [**D3DKMT\_CREATEの割り当てフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createallocationflags)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2_flags)
-   [**D3DKMT\_RELEASEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_releasekeyedmutex2)
-   [**D3DKMTShareObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtshareobjects)

### <a name="span-idcancel_command_interfacespanspan-idcancel_command_interfacespanspan-idcancel_command_interfacespancancel-command-interface"></a><span id="Cancel_command_interface"></span><span id="cancel_command_interface"></span><span id="CANCEL_COMMAND_INTERFACE"></span>Cancel コマンドインターフェイス

-   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand)
-   [**DXGKARG\_CANCELCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_cancelcommand)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)

### <a name="span-idoutput_duplicationspanspan-idoutput_duplicationspanspan-idoutput_duplicationspanoutput-duplication"></a><span id="Output_duplication"></span><span id="output_duplication"></span><span id="OUTPUT_DUPLICATION"></span>出力の重複

-   [**D3DKMTOutputDuplPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplpresent)
-   [**D3DKMTOutputDuplReleaseFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplreleaseframe)
-   [**D3DKMT\_OUTPUTDUPL\_リリース\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_release_frame)
-   [**D3DKMT\_OUTPUTDUPL\_スナップショット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_snapshot)
-   [**D3DKMT\_OUTPUTDUPLCONTEXTSCOUNT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplcontextscount)
-   [**D3DKMT\_OUTPUTDUPLPRESENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresent)
-   [**D3DKMT\_OUTPUTDUPLのフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresentflags)
-   [**D3DKMT\_\_RGNS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_present_rgns)

[**Windows 8 OpenGL の機能強化**](supporting-opengl-enhancements.md)

OpenGL のインストール可能なクライアントドライバー (ICDs) は、新しい関数を呼び出して、リソースへのアクセスを制御し、オブジェクトと識別子の間のマッピングを行うことができます。

 

 





