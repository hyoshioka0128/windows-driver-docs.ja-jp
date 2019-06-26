---
title: OID_GEN_PORT_STATE
description: クエリとしては、上にあるドライバーは、ポート番号、NDIS_OID_REQUEST 構造体のメンバーで指定されているポートの現在の状態を取得するのに OID_GEN_PORT_STATE OID を使用します。
ms.assetid: e0705b2e-08ea-4ed4-a6df-4c33b934c3dd
ms.date: 08/08/2017
keywords: -OID_GEN_PORT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b8f2f8782d2ffc5195f164b7e18855d2ced0e250
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380855"
---
# <a name="oidgenportstate"></a>OID\_GEN\_ポート\_状態


上にあるドライバーが、OID を使用するクエリとして\_GEN\_ポート\_状態 OID で指定されているポートの現在の状態を取得する、 **PortNumber**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS が NDIS を返します、クエリが成功すると、\_状態\_成功し、ポートの状態情報が返されます、 [ **NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)

 

 




