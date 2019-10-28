---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER の状態は、その後のドライバーに対してパケットフィルターが変更されたことを示します。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PACKET_FILTER ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f5f58a7bc534c525334ca42a684d7117868f0574
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842772"
---
# <a name="ndis_status_packet_filter"></a>NDIS\_ステータス\_パケット\_フィルター


NDIS\_STATUS\_パケット\_フィルターの状態は、パケットフィルターがそれまでのドライバーに変更されたことを示します。 NDIS は、ミニポートアダプターのパケットフィルター設定が変更されている可能性があることを通知するために、ミニポートアダプターのこの状態を生成します。

<a name="remarks"></a>注釈
-------

Ndis では、ndis によって NDIS\_ステータス\_パケット\_フィルター状態表示が生成されるときにパケットフィルターが変更されたことを保証しません。

NDIS フィルタードライバーは、NDIS\_ステータス\_パケット\_フィルターの状態の表示を生成することもできます。

NDIS は、 [**ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーで、フィルターの種類のフラグのビットごとの or を提供します。 フィルターの種類のフラグの一覧については、「 [oid\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter) oid」を参照してください。 パケットフィルターの詳細については、「 [OID\_GEN\_サポートされる\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)」を参照してください。

[**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffersize**メンバーが sizeof (ULONG) に設定されています。

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)

[OID\_GEN\_サポート\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)

 

 




