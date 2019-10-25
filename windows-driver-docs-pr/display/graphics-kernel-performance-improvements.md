---
title: グラフィックスカーネルのパフォーマンスの向上
description: グラフィックスハードウェアのパフォーマンスを評価するために、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでは、GPU によって処理される API 呼び出しの正確なタイミング情報をオプションで指定できます。 この機能は Windows 8.1 以降の新機能です。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c10f6e4516b1861964f8f5e9a179353eb41ffd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839671"
---
# <a name="graphics-kernel-performance-improvements"></a>グラフィックスカーネルのパフォーマンスの向上


グラフィックスハードウェアのパフォーマンスを評価するために、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでは、GPU によって処理される API 呼び出しの正確なタイミング情報をオプションで指定できます。 この機能は Windows 8.1 以降の新機能です。

## <a name="span-idkernel_performance_referencespanspan-idkernel_performance_referencespanspan-idkernel_performance_referencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>カーネルパフォーマンスリファレンス


以下の参照トピックでは、ディスプレイミニポートドライバーとユーザーモードの表示ドライバーにこの機能を実装する方法について説明します。

-   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock)
-   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer)
-   [**DXGK\_履歴\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer)
-   [**DXGK\_履歴\_バッファー\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer_header)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_formathistorybuffer)
-   [**DXGKARG\_履歴バッファーの精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_historybufferprecision)
-   [**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)(新しい**DxgkDdiCalibrateGpuClock**メンバーと**DxgkDdiFormatHistoryBuffer**メンバー)
-   [**DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfoflags)の割り当て (新しい**履歴バッファー**のメンバー)
-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype) (new **DXGKQAITYPE\_history bufferprecision**定数値)
-   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) (「解説」の「履歴バッファーの割り当て」を参照してください)

 

 





