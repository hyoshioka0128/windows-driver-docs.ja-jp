---
title: WDDM ドライバーと機能の性能
description: このトピックでは、Windows Display Driver Model (WDDM) ドライバー機能 (cap) について説明します。
ms.assetid: 452ADF64-A5CC-4694-BE31-FBED29B32DC1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984f74aeccd52c71c7c0906b1a9eeca2c6056e0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825197"
---
# <a name="wddm-driver-and-feature-caps"></a>WDDM ドライバーと機能の性能


このトピックでは、Windows Display Driver Model (WDDM) ドライバー機能 (cap) について説明します。

次の表に、ドライバーが WDDM ドライバーの種類とバージョンを指定するための要件を示します。

**WDDM 1.2 ドライバーの要件**

| WDDM ドライバーの種類 | DDI の要件                                                                                                                                                                                                                                           |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 完全なグラフィックス    | レンダリング固有の必要なデバイスドライバーインターフェイス (DDIs) をすべて実装します。                                                                                                                                                            |
| 表示のみ     | すべての表示固有の DDIs を実装し、すべてのレンダリング固有の DDIs に対して null ポインターを返します。                                                                                                                                                         |
| レンダーのみ      | すべてのレンダリング固有の DDIs を実装し、すべての表示固有の DDIs に対して null ポインターを返すか、完全な WDDM ドライバーのすべての DDIs を実装します。ただし、レポート表示\_アダプター\_情報です。NumVidPnSources = 0、\_アダプターの\_情報を表示します。NumVidPnTargets = 0。 |

 

次の表は、Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl) に表示されるすべての機能を示しています。この機能は、WDDM 1.2 ドライバーの設定が必要です。 "M" は必須の機能を示します。 "O" はオプションを示し、"NA" は適用されないことを示します。 各機能の詳細を確認するには、左側の列にあるリンクを参照してください。

**WDDM 1.2 機能キャップ**

| 機能                                                                                                                                          | 完全なグラフィックスドライバー | レンダー専用ドライバー | 表示専用ドライバー | 特徴の上限                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|--------------------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WDDM バージョン                                                                                                                                     | [M]                    | [M]                  | [M]                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**Wddmversion**                                                                                                                                                                |
| [プラグアンドプレイ (pnp) の開始と停止](plug-and-play--pnp--start-and-stop-cases.md): バグチェックと PnP 停止 (VGA 以外) のサポート                   | [M]                    | 該当なし                 | [M]                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**サポート以外の vga**                                                                                                                                                              |
| [最適化された画面ローテーションのサポート](optimized-screen-rotation-support.md)                                                                       | [M]                    | 該当なし                 | [M]                   | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportSmoothRotation**                                                                                                                                                      |
| [GPU プリエンプション](gpu-preemption.md)                                                                                                             | [M]                    | [M]                  | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**PreemptionCaps**                                                                                                                                                             |
| [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)。**FlipOnVSyncMmIo**                                                                                  | [M]                    | [M]                  | 該当なし                  | [**DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)。**FlipOnVSyncMmIoFlipOnVSyncMmIo**は Windows Vista 以降で使用できました。Windows 8 からの要件は、 **FlipOnVSyncMmIo** cap を設定することです。                       |
| [Windows 8 での TDR の変更点](tdr-changes-in-windows-8.md)                                                                                         | [M]                    | [M]                  | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**SupportPerEngineTDR**                                                                                                                                                        |
| [スタンバイ休止状態の最適化](standby-hibernate-optimizations.md): スリープ状態と再開時のパフォーマンスを向上させるためにグラフィックススタックを最適化する | O                    | O                  | 該当なし                  | [**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)。**フラグ**                                                                                                                                                      |
| [ステレオスコピック 3d](stereoscopic-3d.md): ステレオスコピックコンテンツを処理して提示する新しいインフラストラクチャ                                           | O                    | 該当なし                 | 該当なし                  | [**D3DKMDT\_VIDPN\_ソース\_モード\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)                                                                                                                                               |
| [ビデオメモリの直接フリップ](direct-flip-of-video-memory.md)                                                                                   | [M]                    | 該当なし                 | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)。**Supportdirectflip**                                                                                                                                                          |
| [GDI ハードウェアアクセラレーション](gdi-hardware-acceleration.md): WDDM 1.1 以降の必須機能                                            | [M]                    | [M]                  | 該当なし                  | [**DXGK\_のプレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。**SupportKernelModeCommandBuffer**                                                                                                                                 |
| [アイドル状態とアクティブな電源の GPU 電源管理](gpu-power-management-of-idle-and-active-power.md)                                        | O                    | O                  | O                   | この機能がサポートされている場合は、 [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)関数と[*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)関数がサポートされている必要があります。 |

 

 

 





