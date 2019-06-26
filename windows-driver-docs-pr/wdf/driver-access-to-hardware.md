---
title: ハードウェアへのドライバー アクセス
description: ハードウェアへのドライバー アクセス
ms.assetid: 66743284-6cdd-467e-b3b4-3d588cd296a5
keywords:
- PnP WDK KMDF、ハードウェアへのアクセス
- プラグ アンド プレイ WDK KMDF、ハードウェアへのアクセス
- 電源管理 WDK KMDF、ハードウェアへのアクセス
- WDK KMDF ハードウェアへのアクセス
- フレームワークは、WDK KMDF、デバイス オブジェクトをオブジェクトします。
- framework オブジェクト WDK KMDF、ハードウェアへのアクセス
- デバイス オブジェクト WDK KMDF
- WDK KMDF のイベントのコールバック関数
- WDK KMDF のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92ec0e55d1d6ecb0ed7c6a5b319bab0129e92f38
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394108"
---
# <a name="driver-access-to-hardware"></a>ハードウェアへのドライバー アクセス


次の表には、すべてのアルファベット順に、フレームワークのデバイス オブジェクトを定義するイベントのコールバック関数が一覧表示します。 テーブルでは、コールバック関数の WDFDEVICE ハンドルを表すハードウェアをドライバーがアクセスできるコールバック関数を示します。 デバイスが作業 (D0) の状態であるため、ハードウェアにアクセスできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベントのコールバック functionsfor framework デバイス オブジェクト</th>
<th align="left">ハードウェアにアクセスしますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)"><em>EvtDeviceArmWakeFromS0</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)"><em>EvtDeviceArmWakeFromSx</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSxWithReason&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason)"><em>EvtDeviceArmWakeFromSxWithReason</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p>親 bus D0 があります。 デバイスは、D0 にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromS0&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)"><em>EvtDeviceDisarmWakeFromS0</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromSx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)"><em>EvtDeviceDisarmWakeFromSx</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p>親のバスに D0 は、デバイスができない可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)"><em>EvtDeviceFileCreate</em></a></p></td>
<td align="left"><p>状況によって異なる</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterAddResourceRequirements</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterRemoveResourceRequirements</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query)"><em>EvtDeviceRelationsQuery</em></a></p></td>
<td align="left"><p>[はい] が、デバイスがスリープ状態にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources</em></a></p></td>
<td align="left"><p>はい、リソースがデバイスに割り当てられていないが、します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDeviceSelfManagedIoCleanup</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoFlush</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)"><em>EvtDeviceSelfManagedIoInit</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a></p></td>
<td align="left"><p>いいえ、デバイスが削除された場合驚くことにします。それ以外の場合、[はい] です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification)"><em>EvtDeviceUsageNotification</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromS0Triggered&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)"><em>EvtDeviceWakeFromS0Triggered</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromSxTriggered&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)"><em>EvtDeviceWakeFromSxTriggered</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>EvtDeviceWdmIrpPreprocess</em></a></p></td>
<td align="left"><p>IRP に依存します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)"><em>EvtDevicePnpStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePowerPolicyStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification)"><em>EvtDevicePowerPolicyStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification" data-raw-source="[&lt;em&gt;EvtDevicePowerStateChange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)"><em>EvtDevicePowerStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
</tbody>
</table>

 

 

 





