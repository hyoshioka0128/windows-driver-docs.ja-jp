---
title: デバイスがシステムをウェイクできるかどうかの判断
description: デバイスがシステムをウェイクできるかどうかの判断
ms.assetid: 59f23035-4169-4dd4-ac60-882c32efda2c
keywords:
- 待機/ウェイク Irp WDK 電源管理、ウェイクアップ機能を搭載したデバイス
- 電源管理 WDK カーネル、ウェイクアップ機能
- 外部ウェイクアップシグナル WDK
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e0836de1816ec7516f8479d17f58ee03e39b2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828364"
---
# <a name="determining-whether-a-device-can-wake-the-system"></a>デバイスがシステムをウェイクできるかどうかの判断





キーボード、モデム、ネットワークカードなどの一部のデバイスは、デバイスのスリープ状態の間、外部の信号に応答できます。 オペレーティングシステムは、電源管理テクノロジの一部として、このようなデバイスがスリープ状態のシステムをスリープ解除する方法を提供します。これにより、以前のコンテキストを復元できます。 ソフトウェアウェイクアップメカニズムを使用すると、システムとデバイスのハードウェアおよび BIOS のサポートに応じて、S5 (**Powersystemshutdown**) 以外の任意の状態からシステムを起動できます。 状態 S5 のシステムは、常に再起動する必要があります。

オペレーティングシステムはいずれかの中間スリープ状態から復帰するように設計されていますが、正確なウェイクアップ機能はコンピューターやデバイスによって異なります。 すべてのコンピューターがすべてのシステムスリープ状態をサポートしているわけではありません。そのため、一部のコンピューターでは、特定の状態から復帰する機能は無意味です。

同様に、ほとんどのデバイスは、すべてのデバイスの電源状態 (D0 から D3) をサポートしておらず、サポートしているすべてのデバイスの電源状態からのウェイクアップもサポートしていません。

デバイスがウェイクアップをサポートしている状態と共に入力できるスリープ状態は、「バスドライバーによる列挙」で説明されており、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造に格納されています。 次の表に、待機/ウェイクサポートに関連するこの構造体のメンバーを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD1&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD1</strong></a></p></td>
<td><p>デバイスが state PowerDeviceD1 をサポートしている場合は True。</p></td>
</tr>
<tr class="even">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD2&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD2</strong></a></p></td>
<td><p>デバイスが state PowerDeviceD2 をサポートしている場合は True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD0&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD0</strong></a></p></td>
<td><p>デバイスを PowerDeviceD0 からウェイクアップできる場合は True。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD1&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD1</strong></a></p></td>
<td><p>デバイスを PowerDeviceD1 からウェイクアップできる場合は True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD2&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD2</strong></a></p></td>
<td><p>デバイスを PowerDeviceD2 からウェイクアップできる場合は True。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD3&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD3</strong></a></p></td>
<td><p>デバイスを PowerDeviceD3 からウェイクアップできる場合は True。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicestate.md" data-raw-source="[&lt;strong&gt;DeviceState&lt;/strong&gt;](devicestate.md)"><strong>Devicestate</strong></a> [powersystemmaximum]</p></td>
<td><p>このデバイスがシステムの電源状態ごとにサポートできる最高のデバイス電源状態を指定します。 PowerSystemUnspecified から Powersystemunspecified までです。</p></td>
</tr>
<tr class="even">
<td><p><a href="systemwake.md" data-raw-source="[&lt;strong&gt;SystemWake&lt;/strong&gt;](systemwake.md)"><strong>SystemWake</strong></a></p></td>
<td><p>システムの起動に使用する最小のシステム電源の状態 (S0 ~ S4) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicewake.md" data-raw-source="[&lt;strong&gt;DeviceWake&lt;/strong&gt;](devicewake.md)"><strong>DeviceWake</strong></a></p></td>
<td><p>デバイスを目覚めさせることのできるデバイスの電源の最低状態 (D0 ~ D3) を指定します。</p></td>
</tr>
</tbody>
</table>

 

**Devicewake**エントリには、デバイスがウェイクアップ信号に応答できる最も低いデバイス電源状態が一覧表示されます。 PowerDeviceUnspecified の値は、デバイスがシステムをウェイクアップできないことを示します。 **Systemwake**エントリには、システムをウェイクアップできる最小のシステム電源の状態が一覧表示されます。 これらの値は、親 devnode の機能に基づいています。ドライバーで変更することはできません。 詳細については、「[デバイスの電源機能の報告](reporting-device-power-capabilities.md)」を参照してください。

一般に、次の条件に該当する場合、デバイスはシステムをスリープ解除できます。

-   デバイスの電源状態が**Devicewake**値以上になっています。

-   システムの電源状態が**Systemwake**値以上になっています。

 

 




