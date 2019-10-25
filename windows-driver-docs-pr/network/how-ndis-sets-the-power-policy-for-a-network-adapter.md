---
title: NDIS がネットワーク アダプターの電源ポリシーを設定する方法
description: NDIS がネットワーク アダプターの電源ポリシーを設定する方法
ms.assetid: ede0e33d-16f9-45ec-9e9d-b188f6360b2f
keywords:
- ネットワークインターフェイスカード WDK ネットワーク、電源ポリシー
- Nic WDK ネットワーク、電源ポリシー
- 電源ポリシー WDK ネットワーク
- DEVICE_CAPABILITIES
- OID_PNP_CAPABILITIES
- デバイスの電源ポリシー所有者の WDK ネットワーク
- 電源管理 WDK NDIS ミニポート、電源ポリシー
- ユーザー入力の WDK 電源管理
- 電源管理 WDK NDIS ミニポート、ユーザー入力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 781bcb6698977493af8e47e1474150de652ef2e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842540"
---
# <a name="how-ndis-sets-the-power-policy-for-a-network-adapter"></a>NDIS がネットワーク アダプターの電源ポリシーを設定する方法





NDIS は、各ネットワークデバイスのデバイス電源ポリシー所有者として機能します。 そのため、NDIS は各ネットワークデバイスの電源ポリシーを設定し、管理します。 デバイスの電源ポリシーを管理する方法の詳細については、「[デバイスの電源ポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-device-power-policy)」を参照してください。

NDIS では、NIC の電源ポリシーを設定するために次の情報を使用します。

-   [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造。 IRP によって発行された[ **\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)を要求する IRP\_に応答して返されます。

-   NDIS によって発行された、 [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)要求に対するミニポートドライバーの応答。

-   ユーザーインターフェイス (UI) からのユーザー入力。

### <a href="" id="using-the-device-capabilities-structure"></a>デバイス\_機能の構造の使用

NIC が列挙されると、NDIS は、他の要求に加えて、 [**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求を実行して、nic の機能に対してクエリを実行します。 この要求に応答して、バスドライバーは[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造を返します。 NDIS は、この構造をコピーし、NIC の電源ポリシーを設定するときに、この構造の次の情報を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2)">DeviceD1 と DeviceD2</a></p></td>
<td align="left"><p>デバイスが D1 の電源状態をサポートしている場合は TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2" data-raw-source="[DeviceD1 and DeviceD2](https://docs.microsoft.com/windows-hardware/drivers/kernel/deviced1-and-deviced2)">DeviceD1 と DeviceD2</a></p></td>
<td align="left"><p>デバイスが D2 の電源状態をサポートしている場合は TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>デバイスが D0 電源状態のときに外部のウェイクアップ信号に応答できる場合は TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>D1 の電源状態のときに、デバイスが外部ウェイクアップ信号に応答できる場合は TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>D2 電源状態のときに、デバイスが外部ウェイクアップ信号に応答できる場合は TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://docs.microsoft.com/windows-hardware/drivers/kernel/wakefromd0--wakefromd1--wakefromd2--and-wakefromd3)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>D3 電源状態のときに、デバイスが外部ウェイクアップ信号に応答できる場合は TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate" data-raw-source="[DeviceState](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)">Devicestate</a><strong>[powersystemmaximum]</strong></p></td>
<td align="left"><p>このデバイスがシステム電源状態ごとに保持できる、電力が最も高いデバイスの状態を、 <strong>Powersystemunspecified</strong>から<strong>powersystemunspecified</strong>までの間で指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake" data-raw-source="[SystemWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/systemwake)">SystemWake</a></p></td>
<td align="left"><p>デバイスがウェイクイベントに信号を送ることができる、最も電力の低いシステム電源状態 (S0 ~ S4) を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake" data-raw-source="[DeviceWake](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicewake)">DeviceWake</a></p></td>
<td align="left"><p>デバイスがウェイクイベントに信号を送ることができる、デバイスの電力の最低状態 (D0 ~ D3) を指定します。</p></td>
</tr>
</tbody>
</table>

 

NDIS はデバイスの\_機能の情報を使用して、次のことを判断します。

-   システムと NIC の両方で電源管理がサポートされている場合は、システムの電源状態ごとに NIC がどのデバイスの電源の状態にあるかを指定します。

-   システムと NIC はどちらも wake on LAN をサポートしています。その場合、NIC がシステムをスリープ解除できる状態になります。

**WakeFromD0** ~ **WAKEFROMD3**は、NIC がシステムをスリープ解除できるデバイスの電源状態を示します。

**Devicestate**配列は、システムの電源状態ごとに、NIC が可能で、そのシステムの電源状態を引き続きサポートするデバイスの電源状態の最大値を示します。 たとえば、次の配列値について考えてみます。

```cpp
DeviceState[PowerSystemWorking] PowerDeviceD0
DeviceState[PowerSystemSleeping1] PowerDeviceD1
DeviceState[PowerSystemSleeping2] PowerDeviceD2
DeviceState[PowerSystemSleeping3] PowerDeviceD2
DeviceState[PowerSystemHibernate] PowerDeviceD3
DeviceState[PowerSystemShutdown] PowerDeviceD3
```

上記のサンプル値の配列で示されているように、システムの電源状態が S1 の場合、NIC はデバイスの電源状態 D1、D2、または D3 になります。 システムの電源状態が S2 または S3 の場合、NIC はデバイスの電源状態が D2 または D3 であることがあります。

システムと NIC の両方で wake on LAN がサポートされているかどうかを判断するために、NDIS は**systemwake**と**devicewake**の両方のメンバーを調べます。 **Systemwake**と**devicewake**の両方が**powersystemunspecified**に設定されている場合、NDIS は NIC を電源管理に対応するものとして扱います。 この場合、またはミニポートドライバーで NDIS\_属性が設定されている場合、初期化中に\_SUSPEND フラグの\_\_停止しない\_、NDIS はその後ミニポートドライバーに[OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)を発行します。NIC のウェイクアップ機能に関する詳細情報の取得を要求します。

### <a href="" id="using-oid-pnp-capabilities"></a>OID\_PNP\_機能の使用

ミニポートドライバーが[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から正常に復帰すると、次のいずれかに該当する場合、NDIS は、OID\_PNP\_機能の要求をドライバーに送信します。

-   バスドライバーによって返される[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造体の**Systemwake**と**devicewake**の両方のメンバーが**powersystemunspecified**に設定されて*いません*。

-   ミニポートドライバーは、初期化中に[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出したときに、\_SUSPEND フラグに\_\_\_ないように、NDIS\_属性を設定します。

ユーザーが wake on LAN をユーザーインターフェイスで有効にしているかどうかに関係なく、NDIS は、\_の PNP\_機能の要求に OID を発行します。

[OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)のクエリに応答して、ミニポートドライバーが NDIS\_STATUS\_SUCCESS を返した場合、ndis はミニポートドライバーを電源管理対応として扱います。 ミニポートドライバーが NDIS\_STATUS を返し\_\_サポートされていない場合、NDIS は、そのミニポートドライバーを電源管理に対応していない古いミニポートドライバーとして扱います。 このようなドライバーの電源管理の詳細については、「[古いミニポートドライバーの電源管理](power-management-for-old-miniport-drivers.md)」を参照してください。

OID\_PNP\_機能の要求に成功するミニポートドライバーは、要求に応じて次の情報を NDIS に返します。

-   マジックパケットの受信時に NIC がシステムをスリープ解除できる最も低いデバイス電源状態。

-   プロトコルドライバーによって指定されたパターンを含むネットワークフレームを受信したときに NIC がシステムをスリープ解除できる最も低いデバイス電源の状態。

NDIS は、この情報を取得するとすぐに、ユーザーが UI で wake on LAN を有効にした場合に NIC を設定できるデバイスの電源状態を、システムの電源状態ごとに決定します。 NIC がウェイクアップ信号を生成することができる低電力デバイスの状態がない場合 (つまり、デバイス\_機能構造の**Devicestate**配列に指定されているすべての低電力デバイスの電源状態が低い場合)NIC がシステムをスリープ解除できるデバイスの電源状態) NDIS では、 **[電源管理]** タブの nic に対して デバイスがスタンバイ状態から復帰 **[できるよう]** にする オプションが使用されます。 その後、ユーザーは wake on LAN を有効にできません。

**  Wake** on LAN は、NIC とシステムの両方が電源管理に対応している場合にのみ可能です。 システムが電源管理に対応していない場合、NDIS は NIC の電源管理機能に対してクエリを実行しません。

 

### <a name="using-user-input"></a>ユーザー入力の使用

電源管理対応の NIC の場合、Microsoft Windows 2000 以降のバージョンでは、NIC の **[プロパティ]** ダイアログボックスの **[電源管理]** タブで次のオプションを指定できます。

**コンピューターでこのデバイスの電源をオフにして電力を節約できるようにする**

**デバイスがコンピューターをスタンバイ状態から復帰させることを許可する**

最初のオプションは、NIC の電源管理を有効にするために既定で選択されています。 ユーザーがオプションをクリアすると、NDIS は電源管理に関して NIC を古い NIC として扱います。 詳細については、「[古いミニポートドライバーの電源管理](power-management-for-old-miniport-drivers.md)」を参照してください。

2番目のオプションは、既定ではオフになっています。 NDIS によって、NIC がウェイクアップシグナルを生成することが許可されている低電力状態がないと判断した場合、NDIS は2番目のオプションを使用できません。 たとえば、デバイス\_機能構造の**Devicestate**配列メンバーが、すべての低電力システム状態に対して、Nic が D3 に存在する必要があることを示し、 **DEVICESTATE**は、nic のシステムのスリープを解除できるのは D2 です。その後、2番目のチェックボックスは使用できなくなります。

Windows XP と Windows Vista では、上記の2つのオプションに加えて、NIC の **[電源管理]** タブに3つ目のオプションがあります。

**管理ステーションがコンピューターをスタンバイ状態から復帰させることのみを許可する**

このオプションは、前に説明した2番目のオプションの下位にあり、次の場合にのみ使用できます。

-   ユーザーが2番目のオプションを選択して wake on LAN を有効にしました。

-   [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)に応答するミニポートドライバーは、マジックパケットの受信時に NIC がシステムをウェイクアップできることを示しています。

[**管理ステーションにコンピューターをスタンバイから復帰**させる] オプションは、既定ではオフになっています。 ユーザーはこのオプションを選択して、マジックパケットの受信のみによって NIC がシステムにウェイクアップ信号を生成するように指定できます。

ユーザーが NIC の電源管理オプションを選択またはクリアするたびに、システムによって変更が NDIS に通知されます。 NDIS は新しい設定をレジストリに書き込みます。これにより、変更された設定は再起動後も保持されます。

 

 





