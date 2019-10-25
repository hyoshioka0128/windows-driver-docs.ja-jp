---
title: NDIS_STATUS_PM_WAKE_REASON
description: NDIS_STATUS_PM_WAKE_REASON の状態の表示では、ネットワークアダプターによって生成されたウェイクアップイベントに関する情報が提供されます。
ms.assetid: 0CF29C9B-4AAA-473D-A3E8-C1E9530B595E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WAKE_REASON ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 65c6f691911d109e164e91df6d713f22a0f15bfb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843535"
---
# <a name="ndis_status_pm_wake_reason"></a>NDIS\_STATUS\_PM\_WAKE\_REASON


**NDIS\_status\_PM\_wake\_REASON**ステータス表示は、ネットワークアダプターによって生成されたウェイクアップイベントに関する情報を提供します。

<a name="remarks"></a>注釈
-------

NDIS 6.30 以降では、ミニポートドライバーは ndis **\_status\_PM\_ウェイク\_の理由**を示す ndis ステータスを発行します。 この状態表示は、ネットワークアダプターによって生成されたウェイクアップイベントの理由について、NDIS およびそれ以降のドライバーに通知します。

ミニポートドライバーがこの種類の状態の表示をサポートしている場合は、ネットワークアダプターがウェイクアップシグナルを生成したかどうかを示すために、ミニポートドライバーが **\_PM\_wake\_REASON\_状態**を発行する必要があります。 この処理は、アダプターをフルパワー状態に移行するために、 [oid\_PNP\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された OID の oid セット要求を処理している間に行われます。

ミニポートドライバーによってこの状態が示されると、 [**ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーが、 [**ndis\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体へのポインターに設定されます。

**Ndis\_status\_PM\_WAKE\_reason**を発行する方法の詳細については、「 [Ndis Wake reason Status 兆候の発行](https://docs.microsoft.com/windows-hardware/drivers/network/issuing-ndis-wake-reason-indications)」を参照してください。

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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 




