---
title: OID_PNP_CAPABILITIES
description: OID_PNP_CAPABILITIES OID は、ミニポートドライバーに対して、ネットワークアダプターのウェイクアップ機能を返すか、中間ドライバーのウェイクアップ機能を返すための中間ドライバーを要求します。
ms.assetid: f2e3a867-d7d2-4d09-b84b-e8f8610b8535
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_PNP_CAPABILITIES
ms.localizationpriority: medium
ms.openlocfilehash: 00e74bb683c85ca09deecb9190bfd741c459b663
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844042"
---
# <a name="oid_pnp_capabilities"></a>OID\_PNP\_機能


OID\_PNP\_機能 OID は、ネットワークアダプターのウェイクアップ機能を返すためにミニポートドライバーを要求します。または、中間ドライバーのウェイクアップ機能を返すための中間ドライバーを要求します。 ウェイクアップ機能は、次のように定義されている**NDIS\_PNP\_機能**の構造としてフォーマットされています。

```C++
    typedef struct _NDIS_PNP_CAPABILITIES {
         ULONG Flags;
         NDIS_PM_WAKE_UP_CAPABILITIES WakeUpCapabilities;
    } NDIS_PNP_CAPABILITIES, *PNDIS_PNP_CAPABILITIES;  
```




この構造体のメンバーには、次の情報が含まれています。

<a href="" id="flags"></a>**示す**  
**NDIS\_デバイス\_ウェイク\_UP\_ENABLE**

基になるミニポートドライバーが1つ以上のウェイクアップ機能をサポートしている場合、NDIS はこのフラグを設定します。 プロトコルドライバーは、このフラグをテストして、基になるミニポートドライバーにウェイクアップ機能があるかどうかを判断できます。 ミニポートドライバーがこのフラグにアクセスすることはできません。

<a href="" id="wakeupcapabilities"></a>**WakeUpCapabilities**  
ミニポートドライバーのネットワークアダプターのウェイクアップ機能を指定する**NDIS\_PM\_ウェイクアップ\_\_機能**の構造。 **NDIS\_PM\_ウェイク\_UP\_機能**の構造は、次のように定義されています。

```C++
typedef struct _NDIS_PM_WAKE_UP_CAPABILITIES {
         NDIS_DEVICE_POWER_STATE MinMagicPacketWakeUp;
         NDIS_DEVICE_POWER_STATE MinPatternWakeUp;
         NDIS_DEVICE_POWER_STATE MinLinkChangeWakeUp;
       } NDIS_PM_WAKE_UP_CAPABILITIES, *PNDIS_PM_WAKE_UP_CAPABILITIES;
```

この構造体のメンバーには、次の情報が含まれています。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
ミニポートドライバーのネットワークアダプターがマジックパケットの受信時にウェイクアップを通知できる最も低いデバイス電源状態を指定します。 (*マジックパケット*は、受信側のネットワークアダプターのイーサネットアドレスの連続した16個のコピーを含むパケットです)。デバイスの電源状態は、次のいずれかの[**NDIS\_デバイス\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)の値として指定されます。

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
ネットワークアダプターはマジックパケットウェイクアップをサポートしていません。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
ネットワークアダプターは、デバイスの電源状態の D0 からのマジックパケットウェイクアップを通知できます。 D0 は完全な電力状態であるため、ウェイクアップは発生しませんが、実行時イベントとして使用できます。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
ネットワークアダプターは、デバイスの電源状態 D1 および D0 からのマジックパケットウェイクアップを通知できます。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
ネットワークアダプターは、デバイスの状態 D2、D1、および D0 からのマジックパケットウェイクアップを通知できます。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
ネットワークアダプターは、デバイスの電源状態 D3、D2、D1、および D0 からのマジックパケットウェイクアップを通知できます。

<a href="" id="minpatternwakeup"></a>**Minpattern ウェイクアップ**  
プロトコルドライバーによって指定されたパターンを含むネットワークフレームの受信時に、ミニポートドライバーのネットワークアダプターがウェイクアップイベントを通知できる最も小さいデバイスの電源状態を指定します。 電源状態は、次のいずれかの[**NDIS\_デバイス\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)の値として指定されます。

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
ネットワークアダプターは、パターン一致のウェイクアップをサポートしていません。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
ネットワークアダプターは、デバイスの電源状態の D0 からパターン一致のウェイクアップを通知できます。 D0 は完全な電力状態であるため、ウェイクアップは発生しませんが、実行時イベントとして使用できます。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
ネットワークアダプターは、デバイスの電源状態 D1 と D0 からパターン一致のウェイクアップを通知できます。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
ネットワークアダプターは、デバイスの電源状態 D2、D1、および D0 からパターン一致のウェイクアップを通知できます。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
ネットワークアダプターは、デバイスの電源状態 D3、D2、D1、および D0 からパターン一致のウェイクアップを通知できます。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
予約済み。 NDIS は、このメンバーを無視します。

**ミニポートドライバーの場合**

ミニポートドライバーの初期化が完了すると、プロトコルドライバーと NDIS の両方で、この OID でミニポートドライバーを照会して、次のことを判断できます。

-   ミニポートドライバーが PM 対応であるかどうか。

-   ネットワークアダプターのネットワークウェイクアップイベントを示す機能。

ミニポートドライバーが、OID\_PNP\_機能のクエリに対して**ndis\_STATUS\_SUCCESS**を返した場合、ndis はミニポートドライバーを PM 対応と見なします。 ミニポートドライバーが**ndis\_STATUS を返し\_\_サポートされていない**場合、ndis ではミニポートドライバーが、PM 非対応のレガシミニポートドライバーであると見なされます。

[**NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))を呼び出すときに、ウェイクアップ機能をサポートしていないが、電源状態の遷移を通じてネットワークアダプターの状態を保存および復元できるミニポートドライバーは、 **\_SUSPEND フラグの\_\_停止しない\_、NDIS\_属性**を設定できます。 このフラグを設定すると、システムが低電力 (スリープ状態) 状態に移行する前に、NDIS がドライバーの*Miniporthalt*関数を呼び出すことができなくなります。 ただし、ミニポートドライバーが、クエリ OID\_PNP\_機能に応答し**て\_サポートされていない ndis\_ステータス\_** 返された場合、ndis は\_**SUSPEND フラグで ndis\_属性**を無視し\_\_停止し、システムが低電力状態になるとネットワークアダプターを停止します。\_

ミニポートドライバーのネットワークアダプターは、ウェイクアップイベントなど、ウェイクアップイベントの任意の組み合わせをサポートできます。 ミニポートドライバーは、ネットワークアダプターがウェイクアップイベントを通知できない場合でも、電源管理を引き続きサポートできます。 この場合、OID\_PNP\_機能に加えてミニポートドライバーがサポートする唯一の電源管理 Oid は、 [\_pnp\_クエリ\_power](oid-pnp-query-power.md)および[oid\_pnp\_設定\_電力](oid-pnp-set-power.md)です。

ミニポートドライバーのネットワークアダプターで特定のウェイクアップイベントがサポートされていない場合は、 **ndis\_PM\_wake\_up\_CAPABILITIES**構造のウェイクアップイベントについて、 **NdisDeviceStateUnspecified**の[**電源\_状態値\_、ndis\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)がミニポートドライバーによって示される必要があります。

OID\_PNP\_機能は、ミニポートドライバーのネットワークアダプターのウェイクアップ機能のみを示します。このような機能は有効になりません。 [OID\_PNP\_有効にする\_ウェイクアップ\_up](oid-pnp-enable-wake-up.md)を使用して、ネットワークアダプターのウェイクアップ機能を有効にします。

**中間ドライバーの場合**

基になるネットワークアダプターが PM 対応の場合、中間ドライバーは、OID\_PNP\_機能のクエリに対して、 **NDIS\_STATUS\_SUCCESS**を返す必要があります。 この OID によって返される**NDIS\_PM\_wake\_UP\_機能**の構造では、中間ドライバーは、各ウェイクアップ機能 ( **MinMagicPacketWakeUp**または**minpattern ウェイクアップ**) に対して**NdisDeviceStateUnspecified**のデバイスの電源状態を指定する必要があります。 このような応答は、中間ドライバーが PM 対応であり、物理デバイスを管理していないことを示します。

基になるネットワークアダプターが PM を認識していない場合、中間ドライバーは、OID\_PNP\_機能のクエリで**サポート\_されていない NDIS\_の状態\_** 返す必要があります。

詳細について 6.20**は  「** 電源管理機能の[報告](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)」を参照してください。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および NDIS 6.1 でサポートされています。 NDIS 6.20 以降では、代わりに<a href="oid-pm-current-capabilities.md" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](oid-pm-current-capabilities.md)">OID_PM_CURRENT_CAPABILITIES</a>を使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_デバイス\_電源\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))

[OID\_PM\_現在の\_機能](oid-pm-current-capabilities.md)

[\_\_ウェイクアップ\_を有効にする OID\_の PNP](oid-pnp-enable-wake-up.md)

[OID\_PNP\_クエリ\_の機能](oid-pnp-query-power.md)

[OID\_PNP\_設定\_電源](oid-pnp-set-power.md)

[電源管理機能のレポート](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)

 

 




