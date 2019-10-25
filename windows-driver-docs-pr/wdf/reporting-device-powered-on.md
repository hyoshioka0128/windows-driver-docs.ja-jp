---
title: システムが S0 に戻ったときのデバイス電源オンの報告
description: システムが S0 に戻ったときのデバイス電源オンの報告
ms.assetid: 35A48B37-8000-45DC-8E39-4B58ABE7DE68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 978d5244b51c6e40f571856142fc4abb5db930ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842220"
---
# <a name="reporting-device-powered-on-when-system-returns-to-s0"></a>システムが S0 に戻ったときのデバイス電源オンの報告


\[は KMDF にのみ適用され\]

システムが低電力状態から動作中の (S0) 状態に戻ると、PnP マネージャーはシステムセット-電源 IRP ([**irp\_\_セット\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) を送信して、デバイスを動作中の (D0) 状態に戻します。 WDF は、システム設定-電源 IRP を処理します。 ただし、マルチコンポーネントのシナリオでは、ドライバーが電源管理フレームワーク (PoFx) に直接登録されているため、ドライバーは、デバイスが完全オン (D0) 電源への移行を完了したときに[**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出す必要があります。状態. ドライバーは、システムセット-電源 IRP が到着したときに通知を受信するように、WDM 前処理ルーチンを登録することによってこれを実現します。

ドライバーでは、次の手順を使用できます。

1.  [**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を呼び出して、 [**IRP\_に\_電力\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された[*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数を登録します。 コールバックでは、ドライバーはデバイス拡張機能にフラグを設定して、次の[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバックから[**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出す必要があることを示します。
2.  [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)では、フラグが設定されている場合、ドライバーはフラグをクリアし、 [**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出します。
3.  また、ドライバーは[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)のフラグも確認します。 フラグが設定されている場合、デバイスは D0 に戻ることができませんでした。デバイスは削除されています。 この場合、ドライバーは[**Pofxreportdevicepoweredon**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)を呼び出し、その後 power framework で登録を解除します。

 

 





