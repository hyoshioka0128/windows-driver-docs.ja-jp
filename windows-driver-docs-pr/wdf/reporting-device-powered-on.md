---
title: システムが S0 に戻ったときのデバイス電源オンの報告
description: システムが S0 に戻ったときのデバイス電源オンの報告
ms.assetid: 35A48B37-8000-45DC-8E39-4B58ABE7DE68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e458da3c929727fb0c15704e62cdb3bc13f11456
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325196"
---
# <a name="reporting-device-powered-on-when-system-returns-to-s0"></a>システムが S0 に戻ったときのデバイス電源オンの報告


\[KMDF にのみ適用されます。\]

システムは、低電力状態から作業 (S0) の状態に戻ります、PnP マネージャーに送信システム セット-累乗 IRP ([**IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)) を返す作業 (D0) の状態となるデバイス。 WDF 処理システム IRP の出力を設定します。 ただし、マルチ コンポーネントのシナリオでは、ドライバーが直接登録されているため、電源管理フレームワーク (PoFx) をドライバー、呼び出す必要があります[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526)がデバイスの場合完全に入った (D0) 電力状態への移行を完了します。 ドライバーは WDM を登録することによってこれを実現できますセット power IRP が到着する通知システムを受信するルーチンを前処理します。

ドライバーは、次の手順を使用できます。

1.  呼び出す[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043)を登録する、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)用コールバック関数[ **IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)します。 コールバックでは、ドライバーを呼び出す必要があることを示すためにそのデバイスの拡張機能にフラグを設定[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526)から次の[ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック。
2.  [ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)フラグがセットでは、ドライバー、フラグをクリアしますおよび呼び出しの場合、 [ **PoFxReportDevicePoweredOn**](https://msdn.microsoft.com/library/windows/hardware/hh439526)します。
3.  ドライバー、フラグをチェックすることも[ *EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)します。 フラグが設定されている場合は、デバイスが D0 に戻るに失敗し、デバイスが削除されました。 この場合、ドライバーを呼び出す[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526) power framework を使用し、登録を解除します。

 

 





