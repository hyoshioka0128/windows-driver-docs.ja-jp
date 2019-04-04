---
title: OID_PNP_CAPABILITIES
description: OID_PNP_CAPABILITIES OID は、要求のネットワーク アダプターのウェイク アップ機能を返すミニポート ドライバーまたは中間ドライバーのウェイク アップ機能を返す、中間のドライバーを要求します。
ms.assetid: f2e3a867-d7d2-4d09-b84b-e8f8610b8535
ms.date: 08/08/2017
keywords: -OID_PNP_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 80e05b1fa546f0bec9139954c15a4d529a873186
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558491"
---
# <a name="oidpnpcapabilities"></a>OID\_PNP\_機能


OID\_PNP\_機能の OID は、要求のネットワーク アダプターのウェイク アップ機能を返すミニポート ドライバーまたは中間のドライバーのウェイク アップ機能を返す、中間のドライバーを要求します。 ウェイク アップ機能として書式設定、 **NDIS\_PNP\_機能**構造体は、次のように定義されます。

```C++
    typedef struct _NDIS_PNP_CAPABILITIES {
         ULONG Flags;
         NDIS_PM_WAKE_UP_CAPABILITIES WakeUpCapabilities;
    } NDIS_PNP_CAPABILITIES, *PNDIS_PNP_CAPABILITIES;  
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="flags"></a>**フラグ**  
**NDIS\_デバイス\_WAKE\_を\_を有効にします。**

NDIS は、基になるミニポート ドライバーが 1 つまたは複数のウェイク アップ機能をサポートしている場合、このフラグを設定します。 プロトコル ドライバーには、基になるミニポート ドライバーがウェイク アップ機能を持つかどうかを決定するには、このフラグをテストできます。 ミニポート ドライバーでは、このフラグはアクセスしないでください。

<a href="" id="wakeupcapabilities"></a>**WakeUpCapabilities**  
**NDIS\_PM\_WAKE\_を\_機能**ミニポート ドライバーのネットワーク アダプターのウェイク アップ機能を指定する構造体。 **NDIS\_PM\_WAKE\_を\_機能**構造は次のように定義されます。

```C++
typedef struct _NDIS_PM_WAKE_UP_CAPABILITIES {
         NDIS_DEVICE_POWER_STATE MinMagicPacketWakeUp;
         NDIS_DEVICE_POWER_STATE MinPatternWakeUp;
         NDIS_DEVICE_POWER_STATE MinLinkChangeWakeUp;
       } NDIS_PM_WAKE_UP_CAPABILITIES, *PNDIS_PM_WAKE_UP_CAPABILITIES;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
ミニポート ドライバーのネットワーク アダプターがマジック パケットの受信時にウェイク アップを通知デバイスの最下位の電源状態を指定します。 (A*マジック パケット*は受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーを含むパケットです)。デバイスの電源の状態は、次のいずれかとして指定[ **NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)値。

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
ネットワーク アダプターがマジック パケット ウェイク アップの見逃しをサポートしていません。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
ネットワーク アダプターでは、デバイスの電源状態 D0 からマジック パケットのウェイク アップを通知できます。 D0 が完全に電源状態であるため、このウェイク アップ実行されませんが、実行時イベントとして使用できます。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
ネットワーク アダプターでは、デバイスの電源状態 D1 と D0 からマジック パケットのウェイク アップを通知できます。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
ネットワーク アダプターでは、デバイスの状態 D2、D1、および D0 からマジック パケットのウェイク アップを通知できます。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
ネットワーク アダプターでは、デバイスの電源状態 D3、D2、D1、および D0 からマジック パケットのウェイク アップを通知できます。

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
ミニポート ドライバーのネットワーク アダプターがプロトコル ドライバーで指定されたパターンを含むネットワーク フレームの受信時にウェイク アップのイベントを信号最低のデバイスの電源状態を指定します。 電源の状態は、次のいずれかとして指定[ **NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)値。

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
ネットワーク アダプターでは、パターン マッチ ウェイク アップの見逃しはサポートしません。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
ネットワーク アダプターでは、デバイスの電源状態 D0 からパターン マッチのウェイク アップを通知できます。 D0 が完全に電源状態であるため、このウェイク アップ実行されませんが、実行時イベントとして使用できます。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
ネットワーク アダプターでは、D1 と D0 のデバイスの電源状態から、パターン マッチのウェイク アップを通知できます。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
ネットワーク アダプターでは、デバイスの電源状態 D2、D1、および D0 からパターン マッチのウェイク アップを通知できます。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
ネットワーク アダプターでは、D3、D2、D1、および D0 のデバイスの電源状態から、パターン マッチのウェイク アップを通知できます。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
予約済み。 NDIS は、このメンバーは無視されます。

**ミニポート ドライバー**

ミニポート ドライバーには、初期化が完了すると、プロトコル ドライバーおよび NDIS の両方で以下の観点からこの OID のミニポート ドライバーを照会できます。

-   ミニポート ドライバーが PM に対応したかどうか。

-   ネットワーク アダプターの機能を示すはネットワーク ウェイク アップ イベントです。

ミニポート ドライバーに返された場合**NDIS\_状態\_成功**OID のクエリに\_PNP\_機能、NDIS 考慮ミニポート ドライバーで PM に注意してください。 ミニポート ドライバーに返された場合**NDIS\_状態\_いない\_サポートされている**、NDIS ミニポート ドライバーを PM 対応でないレガシ ミニポート ドライバーを検討します。

呼び出すときに[ **NdisMSetAttributesEx**](https://msdn.microsoft.com/library/windows/hardware/ff553623)、ウェイク アップ機能をサポートしていませんが、保存し、電源状態遷移の間でのネットワーク アダプターの状態を復元することができます、ミニポート ドライバーを設定できます、**NDIS\_属性\_いいえ\_HALT\_ON\_SUSPEND**フラグ。 このフラグを設定できなくなります NDIS ドライバーの呼び出し*MiniportHalt* (スリープ) 低電力状態にシステム遷移する前に関数。 ただし、ミニポート ドライバーに返された場合**NDIS\_状態\_いない\_サポートされている**OID のクエリに対する応答で\_PNP\_機能、NDIS 無視、 **NDIS\_属性\_いいえ\_HALT\_ON\_SUSPEND**フラグを設定し、システムが低電力状態になった場合は、ネットワーク アダプターを停止します。

ミニポート ドライバーのネットワーク アダプターには、ウェイク アップ イベント、ウェイク アップ イベントなどの任意の組み合わせをサポートできます。 ネットワーク アダプターにウェイク アップ イベント シグナルをできない場合でも、ミニポート ドライバーは電源管理をサポートもできます。 この場合、唯一の電源管理 OID だけでなく、ミニポート ドライバーをサポートする Oid\_PNP\_機能は[OID\_PNP\_クエリ\_POWER](oid-pnp-query-power.md)と[OID\_PNP\_設定\_POWER](oid-pnp-set-power.md)します。

かどうか、ミニポート ドライバーのネットワーク アダプターは、特定のウェイク アップ イベントをサポートしていない、ミニポート ドライバーが指定する必要があります、 [ **NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)@property **NdisDeviceStateUnspecified**でウェイク アップ イベント、 **NDIS\_PM\_WAKE\_を\_機能**構造体。

OID\_PNP\_機能では、ミニポート ドライバーのウェイク アップ機能のみを示します ' s; のネットワーク アダプターなどの機能を有効にしません。 [OID\_PNP\_を有効にする\_WAKE\_を](oid-pnp-enable-wake-up.md)ネットワーク アダプターのウェイク アップ機能を有効にするために使用します。

**中間ドライバー**

かどうか、基になるネットワーク アダプターが PM 対応で、中間のドライバーが返す必要があります**NDIS\_状態\_成功**OID のクエリに\_PNP\_機能します。 **NDIS\_PM\_WAKE\_を\_機能**構造体がこの OID、によって返される中間のドライバーのデバイスの電源状態を指定する必要があります**NdisDeviceStateUnspecified**ウェイク アップ機能ごと ( **MinMagicPacketWakeUp**または**MinPatternWakeUp**)。 このような応答は、中間のドライバーが PM に対応してが、物理デバイスが管理していないことを示します。

中間のドライバーを返す必要があります、基になるネットワーク アダプターがないかどうか PM に対応した、 **NDIS\_状態\_いない\_サポートされている**OID のクエリに\_PNP\_機能。

**注**  NDIS 6.20 が動作し、それ以降のミニポート ドライバーの電源管理機能を報告する方法については、[電源管理機能の報告](https://msdn.microsoft.com/library/windows/hardware/ff570672)を参照してください。

 

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
<td><p>NDIS 6.0 および 6.1 NDIS でサポートされています。 NDIS 6.20 以降を使用して<a href="oid-pm-current-capabilities.md" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](oid-pm-current-capabilities.md)">OID_PM_CURRENT_CAPABILITIES</a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)

[**NdisMSetAttributesEx**](https://msdn.microsoft.com/library/windows/hardware/ff553623)

[OID\_PM\_現在\_機能](oid-pm-current-capabilities.md)

[OID\_PNP\_を有効にする\_WAKE\_を](oid-pnp-enable-wake-up.md)

[OID\_PNP\_クエリ\_電源](oid-pnp-query-power.md)

[OID\_PNP\_設定\_電源](oid-pnp-set-power.md)

[電源管理機能の報告](https://msdn.microsoft.com/library/windows/hardware/ff570672)

 

 




