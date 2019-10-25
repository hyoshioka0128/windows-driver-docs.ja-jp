---
title: NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES
description: NDIS ミニポートドライバーと MUX 中間ドライバーでは、NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES ステータス表示を使用して、基になる NIC のタスクオフロードハードウェア機能が変更されたことを、NDIS およびそれ以降のドライバーに通知します。
ms.assetid: 9ac8f4c9-66f4-4889-932b-a51381c54734
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: b3f6a6d69cfd53cb06a526615391c6be89acb72e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843505"
---
# <a name="ndis_status_task_offload_hardware_capabilities"></a>NDIS\_ステータス\_タスク\_オフロード\_ハードウェア\_機能


Ndis ミニポートドライバーと MUX 中間ドライバーは、 **ndis\_ステータス\_タスク\_オフロード\_ハードウェア\_機能**の状態の表示を使用して、タスクが変更されたことを ndis およびそれ以降のドライバーに通知します。基になる NIC のハードウェア機能をオフロードします。

<a name="remarks"></a>注釈
-------

基になる NIC を追加または削除した場合は、ミニポートドライバーまたは MUX 中間ドライバーに関連付けられているハードウェア機能の全体的なセットが変更される可能性があります。 たとえば、ミニポートドライバーが NDIS\_ステータス\_タスクを発行する場合は、ハードウェア\_機能の状態の表示 **\_ハードウェア機能の\_オフロード**をサポートしていないことを指定します。これは、サイズの大きい送信オフロード (LSO) をサポートできないことを示します。LSO をサポートするように構成されています。

[**Ndis\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**ndis\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。 この構造体は、タスクのオフロードハードウェア機能を指定します。

タスクオフロードハードウェア機能の詳細については、「 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)」を参照してください。

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


[**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](ndis-status-task-offload-current-config.md)

[OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)

 

 




