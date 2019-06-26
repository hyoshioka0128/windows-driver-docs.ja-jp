---
title: 複数コンポーネントのデバイス、1 つまたは複数の機能の電力状態
description: 1 つまたは複数の機能電源状態を持つ複数コンポーネント デバイスのサポート
ms.assetid: D601A0F6-A035-4161-879A-D495518E7EC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f561c851486b2148b687f119383b7c73a44c648
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368078"
---
# <a name="supporting-multiple-component-devices-with-single-or-multiple-functional-power-states"></a>1 つまたは複数の機能電源状態を持つ複数コンポーネント デバイスのサポート


\[KMDF にのみ適用されます。\]

複数コンポーネントのデバイスの KMDF ドライバーでは、各コンポーネントの 1 つまたは複数の機能の電源状態を定義できます。

この場合、ドライバーは、電源管理フレームワーク (PoFx) と直接登録します。 呼び出し、WDF 登録しないでください、PoFx でドライバーを指定するのには[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)で、 **IdleTimeoutType**のメンバー、 [**WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体を設定**DriverManagedIdleTimeout**. 通常、ドライバーはからには、このメソッドを呼び出してその[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

次に、ドライバーは、PoFx を登録する必要があります。 そのためをドライバーの呼び出しに[ **PoFxRegisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)し[ **PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxstartdevicepowermanagement)します。 デバイスが初めて起動したときに、ドライバーが PoFx を 1 回だけ登録する必要があります。 ドライバーによって提供されるからこれらのルーチンを呼び出すことではこれを行う方法の 1 つ[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)関数。 *EvtDeviceSelfManagedIoInit*最初にデバイスを起動するときにのみと呼びます。

デバイスを削除すると、ドライバーで呼び出す必要があります[ **PoFxUnregisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxunregisterdevice) PoFx からデバイスの登録を解除します。 1 回をお勧めドライバー呼び出しからドライバーによって提供されるこのルーチンのみの登録を解除する[ *EvtDeviceSelfManagedIoFlush* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)関数。 *EvtDeviceSelfManagedIoFlush*デバイスが削除されるときにのみ呼び出されます。 登録を解除して*EvtDeviceSelfManagedIoFlush*ドライバーは、スリープ中に電源登録を保持、および再調整は、遷移し、保留状態のまま I/O 要求の電源の参照を維持する必要はありませんこれらの中に遷移します。

ドライバーを呼び出すと[ *PoFxRegisterDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)を受け取るように、次のトピックで説明されている、PoFx と直接対話に使用できる電源登録ハンドル (POHANDLE)。

-   [コンポーネントの電源状態の I/O 要求の調整](coordinating-i-o-requests-with-component-power-state.md)
-   [デバイスの電源オン S0 にシステムが返されるときにレポートの作成](reporting-device-powered-on.md)
-   [複数コンポーネントのデバイスでのアイドル状態の電源のサポート](supporting-idle-power-down-on-multiple-component-devices.md)

さらに、ドライバーを呼び出すことができます[framework ルーチンの電源を](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)power control の要求を送信して、待機時間の指定に直接保存場所、およびウェイク要件。

PoFx の詳細については、次を参照してください。 [、電源管理フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)します。

 

 





