---
title: 複数コンポーネントのデバイス、1つまたは複数の機能力状態
description: 1 つまたは複数の機能電源状態を持つ複数コンポーネント デバイスのサポート
ms.assetid: D601A0F6-A035-4161-879A-D495518E7EC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41094f0608b3bdc87b25cbca6158680517ad1c26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831739"
---
# <a name="supporting-multiple-component-devices-with-single-or-multiple-functional-power-states"></a>1 つまたは複数の機能電源状態を持つ複数コンポーネント デバイスのサポート


\[は KMDF にのみ適用され\]

複数コンポーネントのデバイス用の KMDF ドライバーでは、コンポーネントごとに1つまたは複数の機能力状態を定義できます。

この場合、ドライバーは、電源管理フレームワーク (PoFx) に直接登録します。 WDF が PoFx に登録されないように指定するには、ドライバーは[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出します。これは、WDF\_\_デバイスの**IdleTimeoutType**メンバーで、[**電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体が**DriverManagedIdleTimeout**に設定されていることを示します。 通常、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数からこのメソッドを呼び出します。

次に、ドライバーを PoFx に登録する必要があります。 これを行うために、ドライバーは[**Pofxregisterdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice)を呼び出し、次に[**Pofxstartdevicepowermanagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxstartdevicepowermanagement)を呼び出します。 デバイスが最初に起動されたときに、ドライバーを PoFx に登録する必要があります。 これを行う1つの方法として、ドライバーによって提供される[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)関数からこれらのルーチンを呼び出すことができます。 *Evtdeviceselfmanagedioinit*は、デバイスが初めて起動されたときにのみ呼び出されます。

デバイスが削除されると、ドライバーは[**Pofxunregisterdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxunregisterdevice)を呼び出して、pofx からデバイスの登録を解除する必要があります。 1回だけ登録を解除するには、ドライバーが提供する[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)関数からこのルーチンを呼び出すことをお勧めします。 *EvtDeviceSelfManagedIoFlush*は、デバイスが削除されるときにのみ呼び出されます。 *EvtDeviceSelfManagedIoFlush*の登録を解除することにより、ドライバーはスリープ中に電源の登録を維持し、切り替え効果を再調整します。また、これらの移行中に保留状態にある i/o 要求の電源参照を維持する必要もありません。

ドライバーは、 [*Pofxregisterdevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)を呼び出すと、次のトピックで説明するように、pofx と直接やり取りするために使用できる電源登録ハンドル (pohandle) を受け取ります。

-   [コンポーネントの電源状態で i/o 要求を調整する](coordinating-i-o-requests-with-component-power-state.md)
-   [システムが S0 に戻ったときに電源がオンになっているレポートデバイス](reporting-device-powered-on.md)
-   [複数コンポーネントのデバイスでのアイドル状態の電源をサポートする](supporting-idle-power-down-on-multiple-component-devices.md)

さらに、ドライバーは、power [framework ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を直接呼び出して、電源管理要求を送信し、待機時間、常駐状態、およびウェイクアップ要件を指定できます。

PoFx の詳細については、「[電源管理フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)」を参照してください。

 

 





