---
title: NDIS_STATUS_PORT_STATE
description: NDIS ポートをサポートするミニポートドライバーは、NDIS_STATUS_PORT_STATE 状態を示し、NDIS ポートの状態の変化を示します。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PORT_STATE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: c25a683fa9e9725af19b6a456022788a7ac1f31a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843532"
---
# <a name="ndis_status_port_state"></a>NDIS\_ステータス\_ポート\_状態


Ndis ポートをサポートするミニポートドライバーは、ndis\_ステータス\_ポート\_状態の状態の表示を使用して、NDIS ポートの状態の変化を示します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体のポート**番号メンバーに**ポート番号を設定する必要があります。 この構造体の**Statusbuffer**メンバーには、 [**NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)構造体へのポインターが含まれています。

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


[**NDIS\_ポート\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 




