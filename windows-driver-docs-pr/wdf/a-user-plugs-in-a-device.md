---
title: ユーザーがデバイスを接続する
description: ユーザーがデバイスを接続する
ms.assetid: cc047c05-f3aa-4423-98fc-cafd7777e104
keywords:
- WDK の PnP KMDF、装置を接続します。
- プラグ アンド プレイ WDK KMDF、装置を接続します。
- WDK KMDF の装置を接続します。
- WDK KMDF のデバイスを追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db4fb925401ceb5f776ea37d5da2b8d749b7ac0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385327"
---
# <a name="a-user-plugs-in-a-device"></a>ユーザーがデバイスを接続する


次のシナリオでは、[デバイス] ノードには、KMDF バス ドライバーと 1 つまたは複数 KMDF 関数またはフィルターをサポートするドライバー、PnP デバイスが含まれます。

ユーザーは、システムの実行中に、バスにデバイスを接続、ときに、デバイスのバス ドライバー、フレームワークは、次のタスクを実行します。

-   デバイスのバス ドライバーを検出し、デバイス呼び出し[ **WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)します。 (このプロセスは「動的な列挙です」と呼ばれます)

-   フレームワークは、バス ドライバーの[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数、バス ドライバーを呼び出せるように[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)物理デバイス (PDO) framework デバイス オブジェクトを作成します。

-   フレームワークは、バス ドライバーの[ *EvtDeviceResourcesQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)と[ *EvtDeviceResourceRequirementsQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)コールバックデバイスを必要とするシステムのハードウェア リソースを特定する関数。

KMDF バス ドライバーの電源投入シーケンスの詳細については、次を参照してください。[バス ドライバーの電源投入シーケンス](power-up-sequence-for-a-bus-driver.md)します。

次に、PnP マネージャーでは、デバイスが必要とする追加のドライバー (関数ドライバーおよびフィルター ドライバー) を決定します。 PnP マネージャーがそれらを読み込み、呼び出しをこれらのドライバーが既に読み込まれていない場合、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン。 各関数またはフィルター ドライバーは、次の操作が行われます。

-   フレームワークは、追加のドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数のドライバーを呼び出すことができるように[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)ドライバーのデバイスを表す framework デバイス オブジェクトを作成します。 関数のドライバーが機能するデバイス オブジェクト (FDO) を作成し、フィルター ドライバーが (フィルターの操作) フィルター デバイス オブジェクトを作成します。

-   フレームワークは各関数とフィルター ドライバーの[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数と、各ドライバーの[ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数。 デバイスが起動して、前に、フレームワークの直前に、 [ *EvtDeviceRemoveAddedResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)コールバック関数。 これら 3 つのコールバック関数では、PnP マネージャーがデバイスにリソースを割り当てる前に、デバイスに必要なハードウェア リソースの一覧を変更するフィルターと関数のドライバーを許可します。 詳細については、次を参照してください[Framework ベースのドライバーのハードウェア リソース。](hardware-resources-for-kmdf-drivers.md)

-   フレームワークにより、デバイスの作業 (D0) の電源状態に達したこと。

-   各関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。
    1.  フレームワークは、ドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) (存在する) 場合、コールバック関数を PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。
    2.  フレームワークは、ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (存在する) 場合、コールバック関数。
    3.  フレームワークは、ドライバーの[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)コールバック関数 (存在する) 場合の各中断し、呼び出し、ドライバーの[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)コールバック関数 (存在する) 場合、ドライバーには、デバイスの割り込みが有効にすることができます。
    4.  場合は、ハードウェアとドライバーは、DMA をサポート、フレームワークのドライバーの[ *EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [ *EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)と[ *EvtDmaEnablerSelfManagedIoStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)コールバックが作成された DMA チャネルごと (存在する) 場合に機能します。
    5.  フレームワークは、ドライバーの[ *EvtChildListScanForChildren* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) (存在する) 場合、コールバック関数。
    6.  フレームワークでは、すべてのデバイスの電源管理対象の I/O キューが開始されます。
    7.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数。

KMDF 関数またはフィルター ドライバーは、電源投入シーケンスの詳細については[関数またはフィルター ドライバーの電源投入シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)します。

 

 





