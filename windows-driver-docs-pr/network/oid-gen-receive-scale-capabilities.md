---
title: OID_GEN_RECEIVE_SCALE_CAPABILITIES
description: クエリとして関連ドライバーを使用できます OID_GEN_RECEIVE_SCALE_CAPABILITIES OID スケーリング (RSS) 機能、NIC とそのミニポート ドライバーの受信側のクエリします。
ms.assetid: b7640ec3-248c-4db2-818d-3976df2dcb9b
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_SCALE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3bd06464c699e3befb5f228fb637d7b326b0d936
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355128"
---
# <a name="oidgenreceivescalecapabilities"></a>OID\_GEN\_受信\_スケール\_機能


クエリとしてドライバーを重なってできます OID を使用\_GEN\_受信\_スケール\_スケーリング (RSS) 機能、NIC とそのミニポート ドライバーの受信側のクエリを実行する機能の OID。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーでは、この OID 要求は表示されません。 NDIS は、ミニポート ドライバーにクエリを処理します。

ミニポート ドライバーは、RSS の機能を返します、 [ **NDIS\_受信\_スケール\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)構造体。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_スケール\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

 

 




