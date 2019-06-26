---
title: OID_GEN_ENUMERATE_PORTS
description: クエリとして NDIS および上にあるドライバーは、基になるミニポート アダプターに関連付けられているアクティブな NDIS ポートの特性を決定するのに OID_GEN_ENUMERATE_PORTS OID を使用します。
ms.assetid: 42a12a05-e360-4493-b037-d3a63906a132
ms.date: 08/08/2017
keywords: -OID_GEN_ENUMERATE_PORTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1c720449c94075208d95308d6c5f870b13f09900
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369112"
---
# <a name="oidgenenumerateports"></a>OID\_GEN\_ENUMERATE\_ポート


クエリとして NDIS と関連付けたドライバーを使用して、OID\_GEN\_ENUMERATE\_基になるミニポート アダプターに関連付けられているアクティブな NDIS ポートの特性を決定するポートの OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS が NDIS を返します、クエリが成功すると、\_状態\_成功でクエリの結果を示し、 [ **NDIS\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)構造体. **NumberOfPorts**の NDIS メンバー\_ポート\_ミニポート アダプターに関連付けられているアクティブなポートの数が配列に含まれています。 **ポート**の NDIS メンバー\_ポート\_配列へのポインターのリストに含まれる[ **NDIS\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造体。 各 NDIS\_ポート\_の特性構造が 1 つの NDIDS ポートの特性を定義します。

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


[**NDIS\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)

[**NDIS\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)

 

 




