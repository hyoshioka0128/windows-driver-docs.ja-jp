---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS ミニポート ドライバーおよび MUX 中間ドライバーは、NDIS に通知する、NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES 状態を示す値を使用し、タスクの変更があった上にあるドライバーは、基になる NIC のハードウェア機能をオフロード
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ecbdd576b12ae9c111945905f1b5ce70a7788312
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372572"
---
# <a name="ndisstatustaskoffloadhardwarecapabilities"></a>NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能


NDIS ミニポート ドライバーと MUX 中間ドライバーの使用、 **NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能**NDIS に通知する状態の表示タスクの変更があった上にあるドライバーは、基になる NIC のハードウェアの機能をオフロードし、

<a name="remarks"></a>注釈
-------

基になる NIC を追加したり削除したり、ミニポート ドライバーまたは MUX 中間ドライバーに関連付けられているハードウェア機能の全体的なセットを変更できます。 たとえば、ミニポート ドライバーの問題、 **NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能**状態を示す値、できないことを指定します。Large Send Offload (LSO)、NIC のサポートは、LSO をサポートするために不要になった構成できます。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。 この構造体は、タスクのオフロード ハードウェア機能を指定します。

タスクのオフロード ハードウェア機能の詳細については、次を参照してください。 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)します。

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


[**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状態\_タスク\_オフロード\_現在\_構成**](ndis-status-task-offload-current-config.md)

[OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)

 

 




