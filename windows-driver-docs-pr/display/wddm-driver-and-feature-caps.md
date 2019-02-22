---
title: WDDM ドライバーと機能の上限
description: このトピックでは、Windows Display Driver Model (WDDM) ドライバー機能 (cap) について説明します。
ms.assetid: 452ADF64-A5CC-4694-BE31-FBED29B32DC1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90692da67e4ce8b062a1952c1ce1c7311dfbcb8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549779"
---
# <a name="wddm-driver-and-feature-caps"></a>WDDM ドライバーと機能の上限


このトピックでは、Windows Display Driver Model (WDDM) ドライバー機能 (cap) について説明します。

このテーブルは、Windows 版の WDDM ドライバーの種類とバージョンを指定するためのドライバーの要件を一覧表示します。

**WDDM 1.2 ドライバーの要件**

| WDDM ドライバーの種類 | DDI 要件                                                                                                                                                                                                                                           |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 完全なグラフィック    | すべてのレンダリングに固有の実装し、表示に固有のデバイス ドライバー インターフェイス (Ddi) が必要です。                                                                                                                                                            |
| 表示のみ     | すべてのディスプレイ固有 Ddi を実装し、すべてのレンダー固有 Ddi の null ポインターを返す                                                                                                                                                         |
| レンダリング専用      | すべてのレンダー固有 Ddi を実装し、すべてのディスプレイ固有 Ddi の null ポインターを返すまたは完全版の WDDM ドライバーのすべての Ddi の実装はレポートの表示\_アダプター\_情報。NumVidPnSources = 0 と表示\_アダプター\_情報。NumVidPnTargets = 0。 |

 

このテーブルには、WDDM 1.2 ドライバーに設定する必要がある Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) に表示されるすべての機能が一覧表示します。 "M"は"O"が、省略可能なことを示します、必須の機能を示すし、"NA"が該当なしを示します。 各機能の詳細を読み取り、左の列で、リンクをクリックします。

**WDDM 1.2 機能キャップ**

| 機能                                                                                                                                          | 完全なグラフィックス ドライバー | 表示専用ドライバー | 表示専用ドライバー | キャップの機能                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|--------------------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WDDM バージョン                                                                                                                                     | M                    | M                  | M                   | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**WDDMVersion**                                                                                                                                                                |
| [プラグ アンド プレイ (PnP) の開始および停止](plug-and-play--pnp--start-and-stop-cases.md):バグ チェックと PnP 停止以外 VGA のサポートします。                   | M                    | 該当なし                 | M                   | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**SupportNonVGA**                                                                                                                                                              |
| [最適化された画面の回転のサポート](optimized-screen-rotation-support.md)                                                                       | M                    | 該当なし                 | M                   | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**SupportSmoothRotation**                                                                                                                                                      |
| [GPU のプリエンプション](gpu-preemption.md)                                                                                                             | M                    | M                  | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**PreemptionCaps**                                                                                                                                                             |
| [**DXGK\_FLIPCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561069).**FlipOnVSyncMmIo**                                                                                  | M                    | M                  | 該当なし                  | [**DXGK\_FLIPCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561069).**FlipOnVSyncMmIoFlipOnVSyncMmIo**が Windows Vista から使用できます。 Windows 8 以降では、要件は、設定する、 **FlipOnVSyncMmIo**キャップ。                       |
| [Windows 8 での TDR の変更](tdr-changes-in-windows-8.md)                                                                                         | M                    | M                  | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**SupportPerEngineTDR**                                                                                                                                                        |
| [スタンバイの最適化を休止](standby-hibernate-optimizations.md):グラフィックス スタックをスリープ状態でパフォーマンスが向上し、再開の最適化 | O                    | O                  | 該当なし                  | [**DXGK\_SEGMENTDESCRIPTOR3**](https://msdn.microsoft.com/library/windows/hardware/hh464086).**フラグ**                                                                                                                                                      |
| [ステレオスコ ピック 3D](stereoscopic-3d.md):プロセスとステレオスコ ピック コンテンツを表示する新しいインフラストラクチャ                                           | O                    | 該当なし                 | 該当なし                  | [**D3DKMDT\_VIDPN\_SOURCE\_MODE\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546727)                                                                                                                                               |
| [ビデオ メモリの直接の反転](direct-flip-of-video-memory.md)                                                                                   | M                    | 該当なし                 | 該当なし                  | [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062).**SupportDirectFlip**                                                                                                                                                          |
| [GDI ハードウェア アクセラレータ](gdi-hardware-acceleration.md):WDDM 1.1 以降に必要な機能                                            | M                    | M                  | 該当なし                  | [**DXGK\_PRESENTATIONCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562004).**SupportKernelModeCommandBuffer**                                                                                                                                 |
| [アイドル状態とアクティブな電源の GPU の電源管理](gpu-power-management-of-idle-and-active-power.md)                                        | O                    | O                  | O                   | この機能がサポートされている場合、 [ *DxgkDdiSetPowerComponentFState* ](https://msdn.microsoft.com/library/windows/hardware/hh451422)と[ *DxgkDdiPowerRuntimeControlRequest* ](https://msdn.microsoft.com/library/windows/hardware/hh451396)関数サポートする必要があります。 |

 

 

 





