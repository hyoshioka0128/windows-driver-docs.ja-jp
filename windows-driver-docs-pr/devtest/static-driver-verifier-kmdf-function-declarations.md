---
title: 静的ドライバー検証ツールでの KMDF 関数の宣言
description: 静的ドライバー検証ツールでの KMDF 関数の宣言
ms.assetid: 1623f3a4-e318-41b3-bbcf-d443202f31e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cbc67327c87323f87060757be75227e95ec4e53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353467"
---
# <a name="static-driver-verifier-kmdf-function-declarations"></a>静的ドライバー検証ツールでの KMDF 関数の宣言


SDV には、KMDF ドライバーを確認するを有効にするにはロールの種類をコールバック関数を使用して各コールバック関数では、宣言する必要があります。 コールバック関数のロールの種類は、さまざまな WDF ヘッダー ファイルで定義されてし、Wdf.h ヘッダー ファイルでは、ドライバーをビルドするとが含まれています。 次の表は、関数のロールの種類と関連付けられているイベントのコールバック関数を示します。

コールバック関数の定義の前に、ドライバーのコールバック関数を宣言する必要があります。 次の例の関数の役割の型宣言を示しています、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 この例では、コールバック関数が呼び出されます*EvtDriverDeviceAdd*します。

```
#include <NTDDK.h>  
#include <wdf.h>
EVT_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
```

コールバック関数に関数のプロトタイプ宣言がある場合とロールの種類の関数の宣言、関数プロトタイプを置き換える必要があります。 関数の役割の種類の宣言に関する詳細については、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

次の表は、コールバック関数の型と関連付けられているイベントのコールバック関数を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ロールの種類の関数</th>
<th align="left">イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540823" data-raw-source="[&lt;em&gt;EvtChildListAddressDescriptionCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540823)"><em>EvtChildListAddressDescriptionCleanup</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_COPY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540824" data-raw-source="[&lt;em&gt;EvtChildListAddressDescriptionCopy&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540824)"><em>EvtChildListAddressDescriptionCopy</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_ADDRESS_DESCRIPTION_DUPLICATE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540836" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionDuplicate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540836)"><em>EvtChildListIdentificationDescriptionDuplicate</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_CREATE_DEVICE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540828" data-raw-source="[&lt;em&gt;EvtChildListCreateDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540828)"><em>EvtChildListCreateDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_DEVICE_REENUMERATED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540830" data-raw-source="[&lt;em&gt;EvtChildListDeviceReenumerated&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540830)"><em>EvtChildListDeviceReenumerated</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540832" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540832)"><em>EvtChildListIdentificationDescriptionCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_COMPARE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540833" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCompare&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540833)"><em>EvtChildListIdentificationDescriptionCompare</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_COPY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540834" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionCopy&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540834)"><em>EvtChildListIdentificationDescriptionCopy</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_CHILD_LIST_IDENTIFICATION_DESCRIPTION_DUPLICATE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540836" data-raw-source="[&lt;em&gt;EvtChildListIdentificationDescriptionDuplicate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540836)"><em>EvtChildListIdentificationDescriptionDuplicate</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_CHILD_LIST_SCAN_FOR_CHILDREN</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540838" data-raw-source="[&lt;em&gt;EvtChildListScanForChildren&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540838)"><em>EvtChildListScanForChildren</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_ARM_WAKE_FROM_S0</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540843" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540843)"><em>EvtDeviceArmWakeFromS0</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_ARM_WAKE_FROM_SX</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540844" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540844)"><em>EvtDeviceArmWakeFromSx</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_DESTROY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_D0_ENTRY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_D0_ENTRY_POST_INTERRUPTS_ENABLED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_D0_EXIT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"><em>EvtDeviceD0Exit</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_D0_EXIT_PRE_INTERRUPTS_DISABLED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_DISABLE_WAKE_AT_BUS</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_DISARM_WAKE_FROM_S0</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540860" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540860)"><em>EvtDeviceDisarmWakeFromS0</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_DISARM_WAKE_FROM_SX</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540862" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540862)"><em>EvtDeviceDisarmWakeFromSx</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_EJECT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_ENABLE_WAKE_AT_BUS</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_FILE_CREATE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540868" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540868)"><em>EvtDeviceFileCreate</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_FILTER_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540870" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540870)"><em>EvtDeviceFilterAddResourceRequirements</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_PNP_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540874" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540874)"><em>EvtDevicePnpStateChange</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_POWER_POLICY_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540874" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540874)"><em>EvtDevicePnpStateChange</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_POWER_STATE_CHANGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540878" data-raw-source="[&lt;em&gt;EvtDevicePowerStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540878)"><em>EvtDevicePowerStateChange</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_PREPARE_HARDWARE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_PROCESS_QUERY_INTERFACE_REQUEST</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540882" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540882)"><em>EvtDeviceProcessQueryInterfaceRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_QUERY_REMOVE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540883" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540883)"><em>EvtDeviceQueryRemove</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_QUERY_STOP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540885" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540885)"><em>EvtDeviceQueryStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_RELATIONS_QUERY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540886" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540886)"><em>EvtDeviceRelationsQuery</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_RELEASE_HARDWARE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"><em>EvtDeviceReleaseHardware</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_REMOVE_ADDED_RESOURCES</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>EvtDeviceRemoveAddedResources</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_RESOURCE_REQUIREMENTS_QUERY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_RESOURCES_QUERY</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"><em>EvtDeviceSelfManagedIoCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_FLUSH</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"><em>EvtDeviceSelfManagedIoFlush</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_INIT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540902" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540902)"><em>EvtDeviceSelfManagedIoInit</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_RESTART</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SELF_MANAGED_IO_SUSPEND</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SET_LOCK</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_SHUTDOWN_NOTIFICATION</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540911" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540911)"><em>EvtDeviceShutdownNotification</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_SURPRISE_REMOVAL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540913" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540913)"><em>EvtDeviceSurpriseRemoval</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_USAGE_NOTIFICATION</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540915" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540915)"><em>EvtDeviceUsageNotification</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DEVICE_WAKE_FROM_S0_TRIGGERED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540919" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromS0Triggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540919)"><em>EvtDeviceWakeFromS0Triggered</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DEVICE_WAKE_FROM_SX_TRIGGERED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540923" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromSxTriggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540923)"><em>EvtDeviceWakeFromSxTriggered</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_DISABLE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_ENABLE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_FILL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"><em>EvtDmaEnablerFill</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_FLUSH</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"><em>EvtDmaEnablerFlush</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DMA_ENABLER_SELFMANAGED_IO_START</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"><em>EvtDmaEnablerSelfManagedIoStart</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DMA_ENABLER_SELFMANAGED_IO_STOP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"><em>EvtDmaEnablerSelfManagedIoStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DPC</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541683" data-raw-source="[&lt;em&gt;EvtDpcFunc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541683)"><em>EvtDpcFunc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_DRIVER_DEVICE_ADD</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541693)"><em>EvtDriverDeviceAdd</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541694" data-raw-source="[&lt;em&gt;EvtDriverUnload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541694)"><em>EvtDriverUnload</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_FILE_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541700" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541700)"><em>EvtFileCleanup</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_FILE_CLOSE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541702" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541702)"><em>EvtFileClose</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_DISABLE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_INTERRUPT_DPC</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541721" data-raw-source="[&lt;em&gt;EvtInterruptDpc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541721)"><em>EvtInterruptDpc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_ENABLE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"><em>EvtInterruptEnable</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_INTERRUPT_ISR</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541735" data-raw-source="[&lt;em&gt;EvtInterruptIsr&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541735)"><em>EvtInterruptIsr</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_SYNCHRONIZE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541742" data-raw-source="[&lt;em&gt;EvtInterruptSynchronize&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541742)"><em>EvtInterruptSynchronize</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_IN_CALLER_CONTEXT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541764" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541764)"><em>EvtIoInCallerContext</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"><em>EvtDestroyCallback</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541756" data-raw-source="[&lt;em&gt;EvtIoCanceledOnQueue&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541756)"><em>EvtIoCanceledOnQueue</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEFAULT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"><em>EvtIoDefault</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"><em>EvtIoDeviceControl</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"><em>EvtIoInternalDeviceControl</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_READ</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"><em>EvtIoRead</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_RESUME</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"><em>EvtIoResume</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_STOP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_WRITE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"><em>EvtIoWrite</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_STATE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541771" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541771)"><em>EvtIoQueueState</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_TARGET_QUERY_REMOVE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541793" data-raw-source="[&lt;em&gt;EvtIoTargetQueryRemove&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541793)"><em>EvtIoTargetQueryRemove</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_TARGET_REMOVE_CANCELED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541800" data-raw-source="[&lt;em&gt;EvtIoTargetRemoveCanceled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541800)"><em>EvtIoTargetRemoveCanceled</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_TARGET_REMOVE_COMPLETE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541806" data-raw-source="[&lt;em&gt;EvtIoTargetRemoveComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541806)"><em>EvtIoTargetRemoveComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_CLEANUP</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_DESTROY</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_PROGRAM_DMA</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541816" data-raw-source="[&lt;em&gt;EvtProgramDma&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541816)"><em>EvtProgramDma</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_REQUEST_CANCEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541817" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541817)"><em>EvtRequestCancel</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_REQUEST_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540745" data-raw-source="[&lt;em&gt;CompletionRoutine&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540745)"><em>CompletionRoutine</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_TIMER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541823" data-raw-source="[&lt;em&gt;EvtTimerFunc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541823)"><em>EvtTimerFunc</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_TRACE_CALLBACK</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_EXECUTE_METHOD</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541836" data-raw-source="[&lt;em&gt;EvtWmiInstanceExecuteMethod&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541836)"><em>EvtWmiInstanceExecuteMethod</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_QUERY_INSTANCE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541843" data-raw-source="[&lt;em&gt;EvtWmiInstanceQueryInstance&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541843)"><em>EvtWmiInstanceQueryInstance</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_INSTANCE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541847" data-raw-source="[&lt;em&gt;EvtWmiInstanceSetInstance&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541847)"><em>EvtWmiInstanceSetInstance</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_ITEM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541852" data-raw-source="[&lt;em&gt;EvtWmiInstanceSetItem&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541852)"><em>EvtWmiInstanceSetItem</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_PROVIDER_FUNCTION_CONTROL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541855" data-raw-source="[&lt;em&gt;EvtWmiProviderFunctionControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541855)"><em>EvtWmiProviderFunctionControl</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WORKITEM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541859" data-raw-source="[&lt;em&gt;EvtWorkItem&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541859)"><em>EvtWorkItem</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDFDEVICE_WDM_IRP_PREPROCESS</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"><em>EvtDeviceWdmIrpPreprocess</em></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionroletypesthatallowmultiplecallbackfunctionsspanspan-idfunctionroletypesthatallowmultiplecallbackfunctionsspanfunction-role-types-that-allow-multiple-callback-functions"></a><span id="function_role_types_that_allow_multiple_callback_functions"></span><span id="FUNCTION_ROLE_TYPES_THAT_ALLOW_MULTIPLE_CALLBACK_FUNCTIONS"></span>複数のコールバック関数を許可する関数のロールの種類

複数のイベント コールバック関数が関連付けられていることのあるいくつかの関数ロールの種類があります。 たとえば、ドライバーが複数をある[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)コールバック関数。 次の表では、機能ロールの種類ごとの SDV をサポートするためのコールバックの最大数を示します。 コールバック関数のテーブルの一覧の最大数よりも多くするためのドライバーに対して正しくない場合は、中には、SDV を使用する場合に、検証プロセスが複雑には。 Sdv map.h ファイルに追加のコールバック関数に対応するために必要な場合があります変更については、次を参照してください。[関数ロールの種類のエントリ ポイントが重複しています](duplicate-entry-points-for-a-function-role-type.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ロールの種類の関数</th>
<th align="left">コールバック関数の最大数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_DPC</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_INTERRUPT_SYNCHRONIZE</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_TIMER</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_EXECUTE_METHOD</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_QUERY_INSTANCE</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_INSTANCE</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_WMI_INSTANCE_SET_ITEM</p></td>
<td align="left"><p>5</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionroletypesandioqueuesspanspan-idfunctionroletypesandioqueuesspanfunction-role-types-and-io-queues"></a><span id="function_role_types_and_i_o_queues"></span><span id="FUNCTION_ROLE_TYPES_AND_I_O_QUEUES"></span>ロールの種類の関数と I/O キュー

宣言するときに次の関数のロールの種類を使用して、[要求ハンドラーの](https://go.microsoft.com/fwlink/p/?linkid=153345)と (順次または並列ディスパッチ) 用ドライバーを I/O 要求を配信するため、KMDF フレームワークに依存するコールバック関数。 手動で、既定のキューからの要求を (手動ディスパッチ) 他のキューに転送する関数をこれらの関数の役割の種類を使用しないでください。 SDV は、1 つのキューからの要求を追跡することを許可するメモリ モデルをサポートしていません。

I/O キューの詳細については、次を参照してください。 [I/O キューの作成](https://go.microsoft.com/fwlink/p/?linkid=153346)です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">手動のディスパッチ用に構成された I/O キューに対して使用されるロールの種類の関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEFAULT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_READ</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_RESUME</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_STOP</p></td>
</tr>
<tr class="even">
<td align="left"><p>EVT_WDF_IO_QUEUE_IO_WRITE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EVT_WDF_IO_QUEUE_STATE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionroletypesfortheevtcleanupcallbackandevtdestroycallbackspanspan-idfunctionroletypesfortheevtcleanupcallbackandevtdestroycallbackspanfunction-role-types-for-the-evtcleanupcallback-and-evtdestroycallback-functions"></a><span id="function_role_types_for_the_evtcleanupcallback_and_evtdestroycallback_"></span><span id="FUNCTION_ROLE_TYPES_FOR_THE_EVTCLEANUPCALLBACK_AND_EVTDESTROYCALLBACK_"></span>関数ロールの種類の EvtCleanupCallback および EvtDestroyCallback 関数

宣言する必要があります、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)と[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)関数ロールの種類のオブジェクトに固有の関数。 SDV は、これらオブジェクトに固有のロールの種類、ドライバーが正しく、コールバック関数を使用しているかどうかを判断する必要があります。 関数を使用するのに種類を決定するのにには、次の表を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクトの種類</th>
<th align="left">EvtCleanupCallback の関数のロールの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_CLEANUP</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/O キュー オブジェクト</p></td>
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイル オブジェクト</p></td>
<td align="left"><p>EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>その他のすべてのオブジェクト</p></td>
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_CLEANUP</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクトの種類</th>
<th align="left">EvDestroyCallback の関数のロールの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>EVT_WDF_DEVICE_CONTEXT_DESTROY</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/O キュー オブジェクト</p></td>
<td align="left"><p>EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイル オブジェクト</p></td>
<td align="left"><p>EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK</p></td>
</tr>
<tr class="even">
<td align="left"><p>その他のすべてのオブジェクト</p></td>
<td align="left"><p>EVT_WDF_OBJECT_CONTEXT_DESTROY</p></td>
</tr>
</tbody>
</table>

 

 

 





