---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: ミニポート ドライバーでは、カプセル化設定の変更があった NDIS と関連付けたドライバーに通知するのに、NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状態を示す値を使用します。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9f066bb82d5fdbc9fddb8a67772a7195944fbf5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383277"
---
# <a name="ndisstatusoffloadencaspulationchange"></a>NDIS\_状態\_オフロード\_カプセル化\_変更


ミニポート ドライバーを使用して、NDIS\_状態\_オフロード\_カプセル化\_カプセル化設定の変更があった NDIS と関連付けたドライバーに通知する状態表示を変更します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)構造体。 NDIS\_オフロード\_カプセル化をカプセル化の設定を指定します。

カプセル化設定の詳細については、次を参照してください。 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)します。

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


[**NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

 

 




