---
title: NDIS がネットワーク アダプターの電源ポリシーを設定する方法
description: NDIS がネットワーク アダプターの電源ポリシーを設定する方法
ms.assetid: ede0e33d-16f9-45ec-9e9d-b188f6360b2f
keywords:
- ネットワーク インターフェイス カード WDK ネットワーク、電源ポリシー
- Nic の WDK ネットワーク、電源ポリシー
- 電源ポリシー WDK ネットワーク
- DEVICE_CAPABILITIES
- OID_PNP_CAPABILITIES
- デバイスの電源ポリシー所有者 WDK ネットワー キング
- WDK の NDIS ミニポート、電源ポリシーの電源管理
- ユーザー入力の WDK 電源管理
- WDK の NDIS ミニポート、ユーザー入力の電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abc803dd36329774f3928581555520aa8fa9a108
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349632"
---
# <a name="how-ndis-sets-the-power-policy-for-a-network-adapter"></a>NDIS がネットワーク アダプターの電源ポリシーを設定する方法





NDIS は、各ネットワーク デバイスのデバイスの電源ポリシー所有者として機能します。 そのため、NDIS は設定して、各ネットワーク デバイスの電源ポリシーを管理します。 デバイスの電源ポリシーの管理に関する詳細については、次を参照してください。[デバイス電源ポリシーを管理する](https://msdn.microsoft.com/library/windows/hardware/ff554355)します。

NDIS では、次の情報を使用して、NIC の電源ポリシーを設定します。

-   [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)への応答を返します、バス ドライバー構造、 [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664) NDIS が発行された要求。

-   ミニポート ドライバーの応答、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)NDIS によって発行された要求。

-   ユーザーのユーザー インターフェイス (UI) から入力します。

### <a href="" id="using-the-device-capabilities-structure"></a>デバイスを使用して\_機能の構造体

NDIS が他の要求だけでなく、発行することにより、NIC の機能をクエリする NIC が列挙されたときに、 [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)要求。 この要求に応答して、バス ドライバーが返されます、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。 NDIS は、この構造体をコピーし、nic、電源ポリシーを設定するときに、この構造体から次の情報を使用

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543085" data-raw-source="[DeviceD1 and DeviceD2](https://msdn.microsoft.com/library/windows/hardware/ff543085)">DeviceD1 と DeviceD2</a></p></td>
<td align="left"><p>デバイス D1 の電源状態をサポートしている場合は TRUE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543085" data-raw-source="[DeviceD1 and DeviceD2](https://msdn.microsoft.com/library/windows/hardware/ff543085)">DeviceD1 と DeviceD2</a></p></td>
<td align="left"><p>デバイス D2 電源の状態をサポートしている場合は TRUE。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565609" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://msdn.microsoft.com/library/windows/hardware/ff565609)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>TRUE の場合、デバイスが外部ウェイク信号 D0 の電源状態のときに応答できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565609" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://msdn.microsoft.com/library/windows/hardware/ff565609)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>TRUE の場合、デバイスが外部ウェイク信号 D1 の電源状態のときに応答できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565609" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://msdn.microsoft.com/library/windows/hardware/ff565609)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>TRUE の場合、デバイスが外部ウェイク信号 D2 の電源状態のときに応答できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565609" data-raw-source="[WakeFromD0, WakeFromD1, WakeFromD2, and WakeFromD3](https://msdn.microsoft.com/library/windows/hardware/ff565609)">WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3</a></p></td>
<td align="left"><p>TRUE の場合、デバイスが外部ウェイク信号 D3 の電源状態のときに応答できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543087" data-raw-source="[DeviceState](https://msdn.microsoft.com/library/windows/hardware/ff543087)">DeviceState</a><strong>[PowerSystemMaximum]</strong></p></td>
<td align="left"><p>このデバイスは、各システムの電源状態から維持できる highest-powered デバイスの状態を指定します<strong>PowerSystemUnspecified</strong>に<strong>PowerSystemShutdown</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564538" data-raw-source="[SystemWake](https://msdn.microsoft.com/library/windows/hardware/ff564538)">SystemWake</a></p></td>
<td align="left"><p>利用した最下位のシステム電源の状態を指定します (S0 S4 を通じて) デバイスが、ウェイク イベントを通知できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543091" data-raw-source="[DeviceWake](https://msdn.microsoft.com/library/windows/hardware/ff543091)">DeviceWake</a></p></td>
<td align="left"><p>最も低い搭載デバイスの電源状態を指定します (D0 D3 を通じて) デバイスが、ウェイク イベントを通知できます。</p></td>
</tr>
</tbody>
</table>

 

デバイスを使用する NDIS\_機能情報を確認します。

-   システムと、NIC の両方が、電源管理をサポートし、場合は、どのデバイスの電源状態が NIC に対して表示される各システム電源の状態。

-   システムと、NIC の両方をサポートして LAN でウェイク アップをし場合は、どのデバイスからの電源状態が、NIC が、システムのスリープを解除します。

**WakeFromD0**を通じて**WakeFromD3** NIC がシステムを起動するデバイスの電源状態を示します。

**DeviceState**配列、各システムの電源状態の highest-powered デバイスの電源の状態を示します、NIC して、まだそのシステムの電源状態をサポートするをします。 たとえば、次の配列の値があるとします。

```cpp
DeviceState[PowerSystemWorking] PowerDeviceD0
DeviceState[PowerSystemSleeping1] PowerDeviceD1
DeviceState[PowerSystemSleeping2] PowerDeviceD2
DeviceState[PowerSystemSleeping3] PowerDeviceD2
DeviceState[PowerSystemHibernate] PowerDeviceD3
DeviceState[PowerSystemShutdown] PowerDeviceD3
```

システムが電源状態 S1 の場合は、サンプルの値の前の配列で示されるように、NIC でデバイスの電源状態 D1、または指定できます d2 に切り替わり、D3 します。 ときに、システムが電源状態 S2 または D2 または D3 のデバイスの電源状態で S3、NIC ができます。

NDIS では、システムと NIC の両方が wake on LAN をサポートするかどうかを確認するのには両方、 **SystemWake**と**DeviceWake**メンバー。 両方**SystemWake**と**DeviceWake**に設定されている**PowerSystemUnspecified**NDIS は、NIC、電源管理の対応として扱います。 この場合、またはミニポート ドライバーの設定、NDIS\_属性\_なし\_停止\_ON\_NDIS、その後、初期化中に中断フラグ ミニポート ドライバーの問題、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)要求、NIC のウェイク アップ機能に関する詳細情報を取得します。

### <a href="" id="using-oid-pnp-capabilities"></a>OID を使用して\_PNP\_機能

後、ミニポート ドライバーが正常に返しますからその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数、NDIS 送信 OID\_PNP\_ドライバーのいずれかの機能要求の以下は true です。

-   両方の**SystemWake**と**DeviceWake**のメンバー、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)によって返される構造体バス ドライバーは*いない*に設定**PowerSystemUnspecified**します。

-   ミニポート ドライバーの設定、NDIS\_属性\_いいえ\_HALT\_ON\_が呼び出されたときに中断フラグ[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)初期化中にします。

NDIS が OID を発行することに注意してください。\_PNP\_、ユーザーがユーザー インターフェイスの LAN のスリープ解除を有効にするかどうかに関係なく、機能要求。

ミニポート ドライバーは、NDIS を返す場合\_状態\_のクエリに対する応答で成功[OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)、NDIS ミニポート ドライバーを電源管理-対応として扱われます。 ミニポート ドライバーは、NDIS を返す場合\_状態\_いない\_サポート、NDIS ミニポート ドライバーとして扱います古いミニポート ドライバーでは、電源管理機能を持つです。 このようなドライバーの電源管理の詳細については、次を参照してください。[古いミニポート ドライバーの電源管理](power-management-for-old-miniport-drivers.md)します。

OID が成功するのミニポート ドライバー\_PNP\_機能要求が要求に応答内の NDIS を次の情報を返します。

-   最小デバイス電源状態、NIC がマジック パケットの受信時にシステムを起動します。

-   最小デバイス電源状態、NIC がプロトコル ドライバーを指定するパターンを含むネットワーク フレームの受信時にシステムを起動します。

NDIS は、この情報を取得、すぐを決定します、各システムの電源状態のデバイスの電源状態 UI でユーザーが wake on LAN が有効になっている場合に、NIC を設定ができます。 許容される低電力デバイスがない場合、NIC がウェイク アップのシグナルを生成の状態 (すべての低電力デバイスの電源状態で指定された場合に、 **DeviceState**デバイスの配列\_機能構造体は、NIC がシステムを起動デバイス電源状態の最も低いより小さい)、NDIS により、**スタンバイからコンピューターの状態にデバイスを許可する**オプション、**電源管理** タブNIC の使用はできません。 次に、ユーザーには、wake on LAN が有効にすることはできません。

**注**  Wake on LAN は、NIC と、システムの両方が電源管理機能を持つ場合にのみ可能です。 システムの電源管理機能を持つは、NDIS は、NIC の電源管理機能をクエリできません。

 

### <a name="using-user-input"></a>ユーザー入力を使用します。

電源管理機能を持つ NIC や Microsoft Windows 2000 以降のバージョンを指定では、次のオプション、**電源管理**の NIC のタブ**プロパティ** ダイアログ ボックス。

**電力を節約するには、このデバイスを無効にするコンピューターを許可します。**

**スタンバイからコンピューターの状態にデバイスを許可します。**

NIC の電源管理を有効にする最初のオプションが既定で選択されます。 オプションをオフにすると、NDIS は電源管理に関して、古い NIC と NIC を扱います。 詳細については、次を参照してください。[古いミニポート ドライバーの電源管理](power-management-for-old-miniport-drivers.md)します。

2 番目のオプションは、既定では明らかです。 NDIS は、許容される低電力状態が、NIC がウェイク アップのシグナルを生成できますがないことを判断した場合 NDIS 2 番目のオプション使用できなくなります。 たとえば場合、 **DeviceState**デバイスの配列メンバー\_機能の構造は、NIC は、すべてのシステムの低電力状態の D3 内でなければならないことを示す場合**DeviceWake**ことを示しますNIC がシステムを解除を利用した最下位のデバイスの状態が d2 に切り替わり、NDIS 網掛けは、2 番目のチェック ボックスを使用できないようにします。

上記の 2 つのオプションだけでなく Windows XP および Windows Vista での 3 番目のオプションが提供、**電源管理**nic タブ。

**管理ステーションは、コンピューターをスタンバイ状態のみを許可します。**

下位に記載されている 2 番目のオプションは、このオプションは使用可能な場合にのみ。

-   ユーザーは、wake on LAN を有効にする 2 つ目のオプションを選択します。

-   応答で、ミニポート ドライバー、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)NIC がマジック パケットの受信時にシステムを wake ことが示されます。

**のみスタンバイからコンピューターを管理局を許可する**オプションが既定でオフです。 ユーザーは、マジック パケットの受信だけがシステムにウェイク アップのシグナルを生成する NIC を発生することを指定するには、このオプションを選択できます。

ユーザーを選択または NIC の電源管理オプションがクリアされるたびに、システムは、変更の NDIS を通知します。 NDIS は、再起動前後で変更された設定が引き続き発生するように、レジストリに新しいに設定を書き込みます。

 

 





