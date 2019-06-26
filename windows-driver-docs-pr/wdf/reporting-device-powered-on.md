---
title: システムが S0 に戻ったときのデバイス電源オンの報告
description: システムが S0 に戻ったときのデバイス電源オンの報告
ms.assetid: 35A48B37-8000-45DC-8E39-4B58ABE7DE68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6caa328539d97cb3a9330a44d6f4943021940bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376292"
---
# <a name="reporting-device-powered-on-when-system-returns-to-s0"></a>システムが S0 に戻ったときのデバイス電源オンの報告


\[KMDF にのみ適用されます。\]

システムは、低電力状態から作業 (S0) の状態に戻ります、PnP マネージャーに送信システム セット-累乗 IRP ([**IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) を返す作業 (D0) の状態となるデバイス。 WDF 処理システム IRP の出力を設定します。 ただし、マルチ コンポーネントのシナリオでは、ドライバーが直接登録されているため、電源管理フレームワーク (PoFx) をドライバー、呼び出す必要があります[ **PoFxReportDevicePoweredOn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)がデバイスの場合完全に入った (D0) 電力状態への移行を完了します。 ドライバーは WDM を登録することによってこれを実現できますセット power IRP が到着する通知システムを受信するルーチンを前処理します。

ドライバーは、次の手順を使用できます。

1.  呼び出す[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を登録する、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)用コールバック関数[ **IRP\_MN\_設定\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)します。 コールバックでは、ドライバーを呼び出す必要があることを示すためにそのデバイスの拡張機能にフラグを設定[ **PoFxReportDevicePoweredOn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)から次の[ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック。
2.  [ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)フラグがセットでは、ドライバー、フラグをクリアしますおよび呼び出しの場合、 [ **PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)します。
3.  ドライバー、フラグをチェックすることも[ *EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)します。 フラグが設定されている場合は、デバイスが D0 に戻るに失敗し、デバイスが削除されました。 この場合、ドライバーを呼び出す[ **PoFxReportDevicePoweredOn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon) power framework を使用し、登録を解除します。

 

 





