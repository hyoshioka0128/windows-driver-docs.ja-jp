---
title: OID_GEN_VLAN_ID
description: クエリとして OID_GEN_VLAN_ID OID が NIC に構成されている VLAN 識別子 (ID) を報告します。
ms.assetid: 4e024951-a578-4f69-873d-879aecc96e68
ms.date: 08/08/2017
keywords: -OID_GEN_VLAN_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c72ace7609c2470cab589219d2fd10dcc943e606
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385732"
---
# <a name="oidgenvlanid"></a>OID\_GEN\_VLAN\_ID


クエリ、OID として\_GEN\_VLAN\_nic ID OID が構成されている VLAN 識別子 (ID) を報告

OID、セットとして\_GEN\_VLAN\_ミニポート ドライバーを処理する NIC の ID OID が構成されている VLAN 識別子 (ID) を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a name="remarks"></a>注釈
-------

この要求で渡された情報バッファーには、NDIS が含まれています\_VLAN\_ID データ型。 この NDIS\_VLAN\_ID 値には、IEEE 802.1 q あたり 12 の最下位ビットで VLAN ID が含まれています-2005 standard。 以降、NDIS のビットを注文\_VLAN\_ID 値は予約されており、0 に設定する必要があります。 NDIS NDIS を定義することに注意してください\_VLAN\_ULONG としての ID。

トランスポートが OID を使用する場合\_GEN\_VLAN\_ミニポート ドライバーのクエリの ID が nic に現在構成されている VLAN ID を返します セットで使用する場合、ミニポート ドライバーは、NIC の現在構成されている VLAN ID を指定した値に設定します。

ミニポート ドライバーの中に[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)特定の NIC ドライバーの関数が最初に、NIC の VLAN ID を 0 に設定します。 ドライバーの*MiniportInitializeEx*関数し、レジストリから次の構成パラメーターを読み取るし、パラメーターが存在する場合は、NIC の VLAN ID をパラメーターの値に設定します。

```syntax
VlanId, REG_DWORD
```

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)

 

 




