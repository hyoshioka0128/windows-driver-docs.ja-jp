---
title: グラフィックス カーネル パフォーマンスの向上
description: グラフィックス ハードウェアのパフォーマンスを評価するには、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできます必要に応じて指定、GPU で処理される API 呼び出しの正確なタイミング情報。 この機能は、新しい Windows 8.1 以降です。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec999bf2141e3683cd8cb206f236e6d41f140e64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323808"
---
# <a name="graphics-kernel-performance-improvements"></a>グラフィックス カーネル パフォーマンスの向上


グラフィックス ハードウェアのパフォーマンスを評価するには、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできます必要に応じて指定、GPU で処理される API 呼び出しの正確なタイミング情報。 この機能は、新しい Windows 8.1 以降です。

## <a name="span-idkernelperformancereferencespanspan-idkernelperformancereferencespanspan-idkernelperformancereferencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>カーネルのパフォーマンスのリファレンス


これらの参照トピックでは、ディスプレイのミニポート ドライバーとユーザー モードのディスプレイ ドライバーでこの機能を実装する方法について説明します。

-   [*DxgkDdiCalibrateGpuClock*](https://msdn.microsoft.com/library/windows/hardware/dn467321)
-   [*DxgkDdiFormatHistoryBuffer*](https://msdn.microsoft.com/library/windows/hardware/dn439360)
-   [**DXGK\_履歴\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/dn439361)
-   [**DXGK\_履歴\_バッファー\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/dn439362)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://msdn.microsoft.com/library/windows/hardware/dn467320)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://msdn.microsoft.com/library/windows/hardware/dn439358)
-   [**DXGKARG\_HISTORYBUFFERPRECISION**](https://msdn.microsoft.com/library/windows/hardware/dn439359)
-   [**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169) (新しい**DxgkDdiCalibrateGpuClock**と**DxgkDdiFormatHistoryBuffer**メンバー)
-   [**DXGK\_ALLOCATIONINFOFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff560966) (新しい**HistoryBuffer**メンバー)
-   [**DXGK\_QUERYADAPTERINFOTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff562010) (新しい**DXGKQAITYPE\_HISTORYBUFFERPRECISION**定数値)
-   [*DxgkDdiCreateAllocation* ](https://msdn.microsoft.com/library/windows/hardware/ff559606) ("「解説」の"履歴バッファーの割り当てを参照してください)

 

 





