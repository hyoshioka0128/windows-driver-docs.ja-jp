---
title: DeviceState
description: DeviceState
ms.assetid: 4cf650ea-cccf-411c-809f-0a01e2ceb067
keywords:
- DeviceState
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 312b01c052f5e67328dccd6a16cf05a2087b7cc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385003"
---
# <a name="devicestate"></a>DeviceState





**DeviceState**のメンバー [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)の配列は、 [**デバイス\_POWER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_device_power_state)値によりインデックス付けされた[**システム\_POWER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_system_power_state)範囲の値**PowerSystemWorking**に**PowerSystemShutdown**します。 配列の各要素には、インデックスで示されるシステム電源の状態のデバイスをサポートできる最大の (highest-powered) デバイスの電源状態が含まれています。 または**PowerDeviceUnspecified**システム電源の状態がサポートされていない場合。

たとえば、S0、S4 および S5 のみをサポートするシステムで[システム電源の状態](system-power-states.md)、 **DeviceState**配列に D0 と D3 の状態のみをサポートするデバイスには、次の表に示すように値が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 要素</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemWorking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemHibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemShutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

すべてのシステム電源の状態をサポートするシステムで、D2 にする必要があるデバイスの配列が含まれる値の状態または削減、システムは、任意の中間に移動するたびに、次の表示しますスリープ状態および状態で、D3 システム hibernaテスト ビルダー。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceState 要素</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemWorking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemHibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceState</strong>[<strong>PowerSystemShutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

注意のエントリ、 **DeviceState**配列は、対応するシステムの電源状態のデバイスをサポートできる最も高いデバイスの電源状態を表します。 前の例では、デバイスでした状態である D3、システム電源の状態のシステム電源の状態の状態の D2 **PowerSystemWorking**を通じて**PowerSystemSleeping3**D1 をシステム状態の状態**PowerSystemWorking**します。

バス ドライバーまたは ACPI フィルターは、親デバイス ノードの機能に基づくこれらの値を設定します。

一般的な規則としてより高度なドライバーはこれらの値を変更しないでください。 ただし、このような変更のために必要なまれな状況で、ドライバーは、バス ドライバーまたは最初に返された ACPI フィルターよりも低い (低電源) 状態を指定できます。 たとえば、ある**DeviceState**\[**PowerSystemSleeping1** \]にマップ**PowerDeviceD2**上の表のようにします。 ドライバーは、この値を変更できる**PowerDeviceD3**には**PowerDeviceD1**または**PowerDeviceD0**します。

 

 




