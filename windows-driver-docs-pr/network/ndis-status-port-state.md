---
title: NDIS_STATUS_PORT_STATE
description: NDIS ポートをサポートするミニポート ドライバーでは、NDIS ポートの状態の変化を示す、NDIS_STATUS_PORT_STATE 状態を示す値を使用します。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PORT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5d2bace5b512b2daae506f60443335fd95fee0a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368534"
---
# <a name="ndisstatusportstate"></a>NDIS\_状態\_ポート\_状態


NDIS ポートをサポートするミニポート ドライバーを使用して、NDIS\_状態\_ポート\_NDIS ポートの状態の変化を示す状態表示の状態。

<a name="remarks"></a>注釈
-------

ミニポート ドライバー ポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。 **StatusBuffer**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)構造体。

<a name="requirements"></a>必要条件
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


[**NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 




