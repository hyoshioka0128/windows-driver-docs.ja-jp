---
title: NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG
description: ミニポート ドライバー、NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG 状態を示す値を使用して、NDIS と関連付けたドライバーに通知されていると、タスクの変更は、NIC の構成をオフロードするには
ms.assetid: 8a098dff-409e-4168-a3aa-372851aa999d
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 26a5655a658ab48030c2bb41e0903e25a7dce706
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361060"
---
# <a name="ndisstatustaskoffloadcurrentconfig"></a>NDIS\_状態\_タスク\_オフロード\_現在\_構成


ミニポート ドライバーを使用して、 **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG** NDIS およびがあった上にあるドライバーに通知する状態を示す値をNIC のタスクのオフロードの構成の変更します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、現在の機能を報告する必要があります、 **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**と現在の状態表示機能を変更します。 この状態を示す値により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。 ミニポート ドライバーは、次の場合にこの状態を示す値を発行する必要があります。

1.  ミニポート ドライバーが受信すると、 [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807)セットの要求の内容を使用する必要があります、 [ **NDIS\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566706)オフロード機能を現在有効になっているタスクを更新する構造体。
2.  ミニポート ドライバーが受信すると、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)セットの要求の内容を使用する必要があります、 [ **NDIS\_オフロード\_カプセル化**](https://msdn.microsoft.com/library/windows/hardware/ff566702)オフロード機能を現在有効になっているタスクを更新する構造体。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造に含まれる、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造体。 発行したときに、 **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**状態を示す値、ミニポート ドライバーを使用する必要があります、 **NDIS\_オフロード**構造体を現在のタスクのオフロード NIC の構成レポート

**注**  の内容、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造のみ、NIC の現在のタスク オフロードの構成、その実際のハードウェアではなくの反映機能。

 

現在のタスク オフロードの構成の詳細については、次を参照してください。 [OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)します。

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


[**NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599)

[**NDIS\_オフロード\_カプセル化**](https://msdn.microsoft.com/library/windows/hardware/ff566702)

[**NDIS\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状態\_タスク\_オフロード\_ハードウェア\_機能**](ndis-status-task-offload-hardware-capabilities.md)

[OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)

[OID\_TCP\_オフロード\_現在\_構成](https://msdn.microsoft.com/library/windows/hardware/ff569805)

[OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807)

 

 




