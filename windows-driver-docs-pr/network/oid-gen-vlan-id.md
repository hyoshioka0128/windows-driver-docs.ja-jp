---
title: OID_GEN_VLAN_ID
description: クエリとして、OID_GEN_VLAN_ID OID は NIC の構成された VLAN 識別子 (ID) を報告します。
ms.assetid: 4e024951-a578-4f69-873d-879aecc96e68
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_VLAN_ID ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: b2c4eb1bc61af459abdb79eeab86f6635fee5a27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844591"
---
# <a name="oid_gen_vlan_id"></a>OID\_GEN\_VLAN\_ID


クエリとして、OID\_GEN\_VLAN\_ID OID は、NIC の構成された VLAN 識別子 (ID) を報告します。

設定として、OID\_GEN\_VLAN\_ID OID は、ミニポートドライバーが処理する NIC の構成された VLAN 識別子 (ID) を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

この要求で渡される情報バッファーには、NDIS\_VLAN\_ID データ型が含まれています。 この NDIS\_VLAN\_ID 値には、IEEE 802.1 Q-2005 標準に従って、下位12ビットの VLAN ID が含まれています。 NDIS\_VLAN\_ID 値の上位ビットは予約されているため、0に設定する必要があります。 NDIS では、NDIS\_VLAN\_ID が ULONG として定義されていることに注意してください。

トランスポートが OID\_GEN\_VLAN\_ID を使用してクエリを実行すると、ミニポートドライバーは NIC に対して現在構成されている VLAN ID を返します。 セットで使用されている場合、ミニポートドライバーは、NIC の現在構成されている VLAN ID を、指定された値に設定します。

特定の NIC に対するミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の実行中に、ドライバーは最初に NIC の VLAN ID をゼロに設定します。 次に、ドライバーの*MiniportInitializeEx*関数は、レジストリから次の構成パラメーターを読み取ります。また、パラメーターが存在する場合は、NIC の VLAN ID をパラメーターの値に設定します。

```syntax
VlanId, REG_DWORD
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

 

 




