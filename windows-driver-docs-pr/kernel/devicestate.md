---
title: DeviceState
description: DeviceState
ms.assetid: 4cf650ea-cccf-411c-809f-0a01e2ceb067
keywords:
- DeviceState
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ce651abbc1813425d239b6c34e0e7abe61d29e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836921"
---
# <a name="devicestate"></a>DeviceState





[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の**devicestate**メンバーは、[**デバイス\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)の値の配列で、[**システム\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)の値から**インデックスが作成されます。Powersystemworking** **Powersystemworking**に使用しています。 配列の各要素には、インデックスによって示されるシステムの電源状態に対してデバイスがサポートできる最大 (高電力) デバイスの電源の状態が含まれます。または、システムの電源状態がサポートされていない場合は**Powerdeviceunspecified**です。

たとえば、S0、S4、および S5[システムの電源状態](system-power-states.md)のみをサポートするシステムでは、D0 および D3 の状態のみをサポートするデバイスの**devicestate**配列には、次の表に示す値が含まれています。

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
<td><p><strong>Devicestate</strong>[<strong>powersystemworking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceUnspecified</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Devicestate</strong>[<strong>powersystemhibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>powersystemshutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

システムの電源状態がすべてサポートされているシステムでは、次の表に示すように、システムが途中のスリープ状態になったとき、またはシステムの hiberna 時に D3 状態になっているデバイスに対して、配列に格納される値の一覧を示します。tes.

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
<td><p><strong>Devicestate</strong>[<strong>powersystemworking</strong>]</p></td>
<td><p><strong>PowerDeviceD0</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping1</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping2</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>PowerSystemSleeping3</strong>]</p></td>
<td><p><strong>PowerDeviceD2</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Devicestate</strong>[<strong>powersystemhibernate</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Devicestate</strong>[<strong>powersystemshutdown</strong>]</p></td>
<td><p><strong>PowerDeviceD3</strong></p></td>
</tr>
</tbody>
</table>

 

**Devicestate**配列のエントリは、デバイスが対応するシステム電源の状態に対してサポートできるデバイスの最大電源状態を示していることに注意してください。 前の例では、システムの電源状態、システム電源状態の**Powersystemworking** ( **PowerSystemSleeping3**)、およびシステム状態**Powersystemworking**の状態 D2 のデバイスが状態 D3 になっている可能性があります。

バスドライバーまたは ACPI フィルターは、親デバイスノードの機能に基づいてこれらの値を設定します。

一般的な規則として、上位レベルのドライバーでは、これらの値を変更しないでください。 ただし、このような変更が必要なまれな状況では、ドライバーは最初に返されたバスドライバーまたは ACPI フィルターよりも低い (電力の低い) 状態を指定できます。 たとえば、上の表に示すように、 **Devicestate**\[**PowerSystemSleeping1**\] が**PowerDeviceD2**にマップされているとします。 ドライバーはこの値を**PowerDeviceD3**に変更できますが、 **PowerDeviceD1**または**PowerDeviceD0**には変更できません。

 

 




