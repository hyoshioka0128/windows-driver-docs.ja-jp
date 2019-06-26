---
title: NDIS_STATUS_OPER_STATUS
description: NDIS_STATUS_OPER_STATUS 状態では、NDIS ドライバーに関連するネットワーク インターフェイスの現在の操作状態を示します。
ms.assetid: dbe7ce19-290d-4a48-a6c2-1b95e956c26c
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OPER_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f303b176eb45e2792d88a6bbe19bf693c90610b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368560"
---
# <a name="ndisstatusoperstatus"></a>NDIS\_状態\_工程\_状態


NDIS\_状態\_工程\_ステータスは、NDIS ドライバーに関連するネットワーク インターフェイスの現在の操作状態を示します。

<a name="remarks"></a>注釈
-------

NDIS が生成されます。 この状態の表示NDIS ミニポート ドライバーでは、この状態を示す値を生成する必要があります。

NDIS の提供、 [ **NDIS\_工程\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)構造体、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。

**StatusBufferSize**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication) sizeof に構造体が設定されている (NDIS\_工程\_状態の場合)。

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


[**NDIS\_工程\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 




