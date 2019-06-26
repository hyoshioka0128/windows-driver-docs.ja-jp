---
title: NDIS_STATUS_PACKET_FILTER
description: NDIS_STATUS_PACKET_FILTER 状態では、ドライバーの後続パケット フィルターの変更を示します。
ms.assetid: 7633772a-cd3d-4030-b97a-9d503341fdeb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PACKET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9b4575a2c0a3aadcf3e00e122f942c0925ff8856
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368547"
---
# <a name="ndisstatuspacketfilter"></a>NDIS\_状態\_パケット\_フィルター


NDIS\_状態\_パケット\_フィルター状態は、ドライバーの後続パケット フィルター変更を示します。 NDIS は、ミニポート アダプターのパケット フィルターの設定の変更が存在する可能性を上にあるドライバーに通知するミニポート アダプターの場合は、この状態インジケーターを生成します。

<a name="remarks"></a>注釈
-------

NDIS は NDIS は、NDIS を生成するときに、パケット フィルターが変更されたことを保証していない\_状態\_パケット\_フィルター状態を示す値。

NDIS フィルター ドライバーでは、NDIS を生成できますも\_状態\_パケット\_フィルター状態を示す値。

NDIS フィルター型フラグのビットごとの OR を提供する、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。 フィルターの型のフラグの一覧は、次を参照してください。、 [OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter) OID。 パケット フィルターの詳細については、次を参照してください。 [OID\_GEN\_サポートされている\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)します。

**StatusBufferSize**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication) sizeof(ULONG) に構造体が設定されています。

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)

[OID\_GEN\_サポートされている\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-packet-filters)

 

 




