---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: ミニポートドライバーは、NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状態表示を使用して、カプセル化の設定が変更されたことを NDIS およびそれ以降のドライバーに通知します。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 3055200cc8aded2fabfdd37773e78c666b45d1f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842779"
---
# <a name="ndis_status_offload_encaspulation_change"></a>NDIS\_ステータス\_オフロード\_暗号化\_変更


ミニポートドライバーは、NDIS\_ステータス\_オフロード\_暗号化\_変更の状態表示を使用して、カプセル化の設定が変更されたことを NDIS およびそれ以降のドライバーに通知します。

<a name="remarks"></a>注釈
-------

[**Ndis\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**NDIS\_オフロード\_カプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造体が含まれています。 NDIS\_OFFLOAD\_カプセル化は、カプセル化の設定を指定します。

カプセル化の設定の詳細については、「 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)」を参照してください。

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


[**NDIS\_OFFLOAD\_のカプセル化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_オフロード\_のカプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

 

 




