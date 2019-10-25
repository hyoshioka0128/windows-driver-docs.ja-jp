---
title: ユーザーがデバイスに接続する
description: ユーザーがデバイスに接続する
ms.assetid: cc047c05-f3aa-4423-98fc-cafd7777e104
keywords:
- PnP WDK KMDF、デバイスの接続
- WDK KMDF のプラグアンドプレイ、デバイスの接続
- デバイスへの接続 (WDK KMDF)
- WDK KMDF デバイスの追加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c006e5a8699a8573ca468b9d98d7457a69bd78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841674"
---
# <a name="a-user-plugs-in-a-device"></a>ユーザーがデバイスに接続する


次のシナリオでは、デバイスノードに KMDF バスドライバーと、PnP デバイスをサポートする1つ以上の KMDF 関数またはフィルタードライバーが含まれています。

システムの実行中にユーザーがデバイスをバスに接続すると、デバイスのバスドライバーとフレームワークは次のタスクを実行します。

-   デバイスのバスドライバーによってデバイスが検出され、 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)が呼び出されます。 (このプロセスは "動的列挙" と呼ばれます)。

-   フレームワークはバスドライバーの[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数を呼び出します。そのため、バスドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、物理デバイス (PDO) のフレームワークデバイスオブジェクトを作成できます。

-   このフレームワークは、バスドライバーの[*EvtDeviceResourcesQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)および[*EvtDeviceResourceRequirementsQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)コールバック関数を呼び出して、デバイスに必要なシステムハードウェアリソースを決定します。

KMDF バスドライバーの電源投入シーケンスの詳細については、「[バスドライバーの電源をオン](power-up-sequence-for-a-bus-driver.md)にする」を参照してください。

次に、PnP マネージャーによって、デバイスに必要な追加のドライバー (関数ドライバーとフィルタードライバー) が決定されます。 これらのドライバーがまだ読み込まれていない場合は、PnP マネージャーによってそれらが読み込まれ、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンが呼び出されます。 関数またはフィルタードライバーごとに、次のアクションが実行されます。

-   このフレームワークは、追加のドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出します。これにより、ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、ドライバーのデバイスを表すフレームワークデバイスオブジェクトを作成できるようになります。 関数ドライバーは、機能しているデバイスオブジェクト (FDO) を作成し、フィルタードライバーはフィルターデバイスオブジェクト (フィルター処理) を作成します。

-   フレームワークは、各関数とフィルタードライバーの[*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) callback 関数を呼び出し、その後、各ドライバーの[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数を呼び出します。 デバイスが起動する直前に、フレームワークは[*Evtdeviceremoveaddedresources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)コールバック関数を呼び出します。 これら3つのコールバック関数を使用すると、PnP マネージャーがデバイスにリソースを割り当てる前に、フィルターおよび関数ドライバーで、デバイスに必要なハードウェアリソースの一覧を変更できます。 詳細については、「[フレームワークベースのドライバーのハードウェアリソース](hardware-resources-for-kmdf-drivers.md)」を参照してください。

-   このフレームワークにより、デバイスが動作 (D0) の電源状態に達したことが確認されます。

-   デバイスをサポートする関数とフィルタードライバーごとに、次の処理が実行されます。これは、ドライバースタックの一番下にあるドライバーから、一度に1つずつ実行されます。
    1.  フレームワークは、ドライバーの[*Evtdeviceの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数 (存在する場合) を呼び出し、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースのリストを渡します。
    2.  フレームワークは、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)コールバック関数 (存在する場合) を呼び出します。
    3.  フレームワークは、各割り込みのドライバーの[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) callback 関数 (存在する場合) を呼び出し、ドライバーの[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled) callback 関数 (存在する場合) を呼び出して、ドライバーが有効にできるようにします。デバイスの割り込み。
    4.  ハードウェアとドライバーが DMA をサポートしている場合、フレームワークは、作成された各 DMA チャネルに対して、ドライバーの[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)、および[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)のコールバック関数 (存在する場合) を呼び出します。
    5.  フレームワークは、ドライバーの[*Evtchildlistscanforchildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)コールバック関数 (存在する場合) を呼び出します。
    6.  フレームワークは、デバイスのすべての電源管理 i/o キューを開始します。
    7.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[*Evtdeviceselfmanagedioinit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)コールバック関数を呼び出します。

KMDF 関数またはフィルタードライバーの電源投入シーケンスの詳細については、[関数またはフィルタードライバーの電源を](power-up-sequence-for-a-function-or-filter-driver.md)入れてください。

 

 





