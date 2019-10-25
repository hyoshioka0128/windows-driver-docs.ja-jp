---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状態表示を使用して、NIC のタスクオフロード構成が変更されたことを NDIS およびそれ以降のドライバーに通知します。
ms.assetid: 8a098dff-409e-4168-a3aa-372851aa999d
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e4dfff15f00209884b882ab74ce996dd2815b273
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843509"
---
# <a name="ndis_status_task_offload_current_config"></a>NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成


ミニポートドライバーは、 **ndis\_STATUS\_タスク\_オフロード\_現在の\_構成**の状態の表示を使用して、NIC のタスクオフロード構成が変更されたことを ndis およびそれ以降のドライバーに通知します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、現在の機能が変更されたときに、現在の\_構成の状態を示す **\_タスク\_オフロード\_\_** 、現在の機能を使用して、現在の機能を報告する必要があります。 この状態の表示により、すべてのプロトコルドライバーが新機能の情報で更新されます。 次の場合に、この状態を示すミニポートドライバーが必要です。

1.  ミニポートドライバーが[\_TCP\_オフロード\_parameters](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) set 要求の OID を受信する場合、現在有効になっているタスクオフロードを更新するには、 [**NDIS\_offload\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体の内容を使用する必要があります機能.
2.  ミニポートドライバーが[OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)セット要求を受信する場合、現在有効になっているタスクオフロードを更新するには、 [**NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造の内容を使用する必要があります機能.

[**Ndis\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**ndis\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。 **Ndis\_status\_タスク**を発行するときに、現在の\_構成の状態を示す\_オフロード\_、ミニポートドライバーでは、現在のタスクオフロード構成を報告するために、 **ndis\_offload**構造体を使用する必要があります。NIC の。

[**NDIS\_のオフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造の内容は、実際のハードウェア機能ではなく、NIC の現在のタスクオフロード構成のみを反映している  に**注意**してください。

 

現在のタスクオフロード構成の詳細については、「 [OID\_TCP\_オフロード\_現在の\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)」を参照してください。

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

[**NDIS\_OFFLOAD\_のカプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_ステータス\_タスク\_オフロード\_ハードウェア\_機能**](ndis-status-task-offload-hardware-capabilities.md)

[OID\_オフロード\_のカプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

[OID\_TCP\_オフロード\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)

[OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)

 

 




