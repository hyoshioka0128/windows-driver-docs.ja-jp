---
title: デバイスがシステムをウェイクできるかどうかの判断
description: デバイスがシステムをウェイクできるかどうかの判断
ms.assetid: 59f23035-4169-4dd4-ac60-882c32efda2c
keywords:
- 待機/ウェイク Irp WDK 電源管理では、ウェイク アップ機能を持つデバイス
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9d4a32b4715d571f372dbd4188aec767440af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580254"
---
# <a name="determining-whether-a-device-can-wake-the-system"></a>デバイスがシステムをウェイクできるかどうかの判断





キーボード、モデム、およびネットワーク カードなど、一部のデバイスは、デバイスのスリープ状態の間の外部のシグナルに対応できます。 電源管理テクノロジの一部としては、オペレーティング システムは、このようなデバイスの以前のコンテキストを復元することができます、スリープ状態のシステムをスリープ解除する方法を提供します。 ソフトウェアのウェイク アップ メカニズムにより、システム S5 を除く任意の状態から再開する (**PowerSystemShutdown**)、システムとデバイスのハードウェアおよび BIOS でのサポートによって異なります。 S5 の状態でシステムを再起動することが常にあります。

オペレーティング システムから中間のスリープ状態のいずれかがスリープ解除するよう設計されていますが、コンピューターから別のコンピューターとデバイスに正確なウェイク アップ機能が異なります。 すべてのシステム スリープ状態をサポートしていないすべてのコンピューターそのため、特定の状態からスリープ解除する機能は、一部のコンピューターでは無意味です。

同様に、ほとんどのデバイスは、すべてのデバイスの電源の状態もをサポート (D3 を通じて D0) もサポート ウェイク アップのすべてのデバイスの電源をサポートする状態。

スリープは、元のことをスリープ解除をサポート、バス ドライバーによって列挙で説明されていると状態に格納されますと共に、デバイスを入力できることを示す、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。 次の表は、サポートの待機またはスリープ解除に関連するこの構造体のメンバーを一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD1&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD1</strong></a></p></td>
<td><p>デバイス状態 PowerDeviceD1 をサポートしている場合は true。</p></td>
</tr>
<tr class="even">
<td><p><a href="deviced1-and-deviced2.md" data-raw-source="[&lt;strong&gt;DeviceD2&lt;/strong&gt;](deviced1-and-deviced2.md)"><strong>DeviceD2</strong></a></p></td>
<td><p>デバイス状態 PowerDeviceD2 をサポートしている場合は true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD0&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD0</strong></a></p></td>
<td><p>デバイスが PowerDeviceD0 からウェイクできる場合は true。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD1&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD1</strong></a></p></td>
<td><p>デバイスが PowerDeviceD1 からウェイクできる場合は true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD2&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD2</strong></a></p></td>
<td><p>デバイスが PowerDeviceD2 からウェイクできる場合は true。</p></td>
</tr>
<tr class="even">
<td><p><a href="wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md" data-raw-source="[&lt;strong&gt;WakeFromD3&lt;/strong&gt;](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)"><strong>WakeFromD3</strong></a></p></td>
<td><p>デバイスが PowerDeviceD3 からウェイクできる場合は true。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicestate.md" data-raw-source="[&lt;strong&gt;DeviceState&lt;/strong&gt;](devicestate.md)"><strong>DeviceState</strong> </a> [PowerSystemMaximum]</p></td>
<td><p>このデバイスをサポートできる PowerSystemShutdown に PowerSystemUnspecified から各システムの電源状態の最大のデバイスの電源状態を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="systemwake.md" data-raw-source="[&lt;strong&gt;SystemWake&lt;/strong&gt;](systemwake.md)"><strong>SystemWake</strong></a></p></td>
<td><p>最小のシステムの電源を指定します (を通じて S4 は S0) の状態、システムを起動できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="devicewake.md" data-raw-source="[&lt;strong&gt;DeviceWake&lt;/strong&gt;](devicewake.md)"><strong>DeviceWake</strong></a></p></td>
<td><p>最下位のデバイスの電源を指定します (D3 を通じて D0) の状態、デバイスが再開できます。</p></td>
</tr>
</tbody>
</table>

 

**DeviceWake**エントリには、元のデバイスがウェイク アップ信号に応答できる最小のデバイスの電源状態が一覧表示されます。 PowerDeviceUnspecified 値では、デバイスが、システムのスリープを解除できないことを示します。 **SystemWake**エントリには、元のシステムを起動できます最も低いシステム電源の状態が一覧表示されます。 これらの値は親 devnode の機能に基づいており、ドライバーは変更はできません。 詳細については、次を参照してください。[デバイスの電源機能の報告](reporting-device-power-capabilities.md)します。

一般に、デバイスは、次の条件に当てはまる場合に、システムをスリープ解除できます。

-   デバイスが電源の状態と等しいかよりも詳細を利用した、 **DeviceWake**値。

-   システムが電源の状態と等しいかそれよりも電源が投入されて、 **SystemWake**値。

 

 




