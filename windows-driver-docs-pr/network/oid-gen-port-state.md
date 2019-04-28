---
title: OID_GEN_PORT_STATE
description: クエリとしては、上にあるドライバーは、ポート番号、NDIS_OID_REQUEST 構造体のメンバーで指定されているポートの現在の状態を取得するのに OID_GEN_PORT_STATE OID を使用します。
ms.assetid: e0705b2e-08ea-4ed4-a6df-4c33b934c3dd
ms.date: 08/08/2017
keywords: -OID_GEN_PORT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6349425aff9bb0a08bd6b14f85076eda1c2a6d19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367584"
---
# <a name="oidgenportstate"></a>OID\_GEN\_ポート\_状態


上にあるドライバーが、OID を使用するクエリとして\_GEN\_ポート\_状態 OID で指定されているポートの現在の状態を取得する、 **PortNumber**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS が NDIS を返します、クエリが成功すると、\_状態\_成功し、ポートの状態情報が返されます、 [ **NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)構造体。

<a name="requirements"></a>要件
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


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)

 

 




