---
title: ハードウェアへのドライバー
description: ハードウェアへのドライバー
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
ms.openlocfilehash: bcef70cb291c05c242dda3bc4721dc558047b931
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535385"
---
# <a name="driver-access-to-hardware"></a>ハードウェアへのドライバー


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540843" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540843)"><em>EvtDeviceArmWakeFromS0</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540844" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540844)"><em>EvtDeviceArmWakeFromSx</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540846" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSxWithReason&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540846)"><em>EvtDeviceArmWakeFromSxWithReason</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"><em>EvtDeviceD0Exit</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus</em></a></p></td>
<td align="left"><p>親 bus D0 があります。 デバイスは、D0 にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540860" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540860)"><em>EvtDeviceDisarmWakeFromS0</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540862" data-raw-source="[&lt;em&gt;EvtDeviceDisarmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540862)"><em>EvtDeviceDisarmWakeFromSx</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus</em></a></p></td>
<td align="left"><p>親のバスに D0 は、デバイスができない可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540868" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540868)"><em>EvtDeviceFileCreate</em></a></p></td>
<td align="left"><p>状況によって異なる</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540870" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540870)"><em>EvtDeviceFilterAddResourceRequirements</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540872" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540872)"><em>EvtDeviceFilterRemoveResourceRequirements</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540886" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540886)"><em>EvtDeviceRelationsQuery</em></a></p></td>
<td align="left"><p>[はい] が、デバイスがスリープ状態にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"><em>EvtDeviceReleaseHardware</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>EvtDeviceRemoveAddedResources</em></a></p></td>
<td align="left"><p>はい、リソースがデバイスに割り当てられていないが、します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"><em>EvtDeviceSelfManagedIoCleanup</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"><em>EvtDeviceSelfManagedIoFlush</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540902" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540902)"><em>EvtDeviceSelfManagedIoInit</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a></p></td>
<td align="left"><p>いいえ、デバイスが削除された場合驚くことにします。それ以外の場合、[はい] です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540913" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540913)"><em>EvtDeviceSurpriseRemoval</em></a></p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540915" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540915)"><em>EvtDeviceUsageNotification</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540919" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromS0Triggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540919)"><em>EvtDeviceWakeFromS0Triggered</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540923" data-raw-source="[&lt;em&gt;EvtDeviceWakeFromSxTriggered&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540923)"><em>EvtDeviceWakeFromSxTriggered</em></a></p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"><em>EvtDeviceWdmIrpPreprocess</em></a></p></td>
<td align="left"><p>IRP に依存します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540874" data-raw-source="[&lt;em&gt;EvtDevicePnpStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540874)"><em>EvtDevicePnpStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540876" data-raw-source="[&lt;em&gt;EvtDevicePowerPolicyStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540876)"><em>EvtDevicePowerPolicyStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540878" data-raw-source="[&lt;em&gt;EvtDevicePowerStateChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540878)"><em>EvtDevicePowerStateChange</em></a></p></td>
<td align="left"><p>状態によって異なります。</p></td>
</tr>
</tbody>
</table>

 

 

 





