---
title: グラフィックス カーネル パフォーマンスの向上
description: グラフィックス ハードウェアのパフォーマンスを評価するには、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできます必要に応じて指定、GPU で処理される API 呼び出しの正確なタイミング情報。 この機能は、新しい Windows 8.1 以降です。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8a984f3052b84b9c5aa5b2787b280151b7c4af2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379930"
---
# <a name="graphics-kernel-performance-improvements"></a>グラフィックス カーネル パフォーマンスの向上


グラフィックス ハードウェアのパフォーマンスを評価するには、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできます必要に応じて指定、GPU で処理される API 呼び出しの正確なタイミング情報。 この機能は、新しい Windows 8.1 以降です。

## <a name="span-idkernelperformancereferencespanspan-idkernelperformancereferencespanspan-idkernelperformancereferencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>カーネルのパフォーマンスのリファレンス


これらの参照トピックでは、ディスプレイのミニポート ドライバーとユーザー モードのディスプレイ ドライバーでこの機能を実装する方法について説明します。

-   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock)
-   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer)
-   [**DXGK\_履歴\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer)
-   [**DXGK\_履歴\_バッファー\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer_header)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_formathistorybuffer)
-   [**DXGKARG\_HISTORYBUFFERPRECISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_historybufferprecision)
-   [**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data) (新しい**DxgkDdiCalibrateGpuClock**と**DxgkDdiFormatHistoryBuffer**メンバー)
-   [**DXGK\_ALLOCATIONINFOFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfoflags) (新しい**HistoryBuffer**メンバー)
-   [**DXGK\_QUERYADAPTERINFOTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype) (新しい**DXGKQAITYPE\_HISTORYBUFFERPRECISION**定数値)
-   [*DxgkDdiCreateAllocation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) ("「解説」の"履歴バッファーの割り当てを参照してください)

 

 





