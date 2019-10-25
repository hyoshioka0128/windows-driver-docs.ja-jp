---
title: OID_GEN_RECEIVE_SCALE_CAPABILITIES
description: クエリとして、後続のドライバーは OID_GEN_RECEIVE_SCALE_CAPABILITIES OID を使用して、NIC とそのミニポートドライバーの RECEIVE side scaling (RSS) 機能を照会できます。
ms.assetid: b7640ec3-248c-4db2-818d-3976df2dcb9b
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_RECEIVE_SCALE_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 71c7dd1837db03e419f048c01549775854b481d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840476"
---
# <a name="oid_gen_receive_scale_capabilities"></a>OID\_GEN\_\_スケール\_の機能の受信


クエリとして、それ以降のドライバーでは、OID\_GEN\_RECEIVE\_SCALE\_機能 OID を使用して、NIC とそのミニポートドライバーの receive side scaling (RSS) 機能を照会できます。

<a name="remarks"></a>注釈
-------

NDIS ミニポートドライバーは、この OID 要求を受信しません。 NDIS はミニポートドライバーのクエリを処理します。

ミニポートドライバーは、 [**NDIS\_RECEIVE\_SCALE\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)構造体の RSS 機能を返します。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_スケール\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

 

 




