---
title: OID_GEN_PORT_STATE
description: クエリとして、後続のドライバーは OID_GEN_PORT_STATE OID を使用して、NDIS_OID_REQUEST 構造体のポート番号メンバーに指定されているポートの現在の状態を取得します。
ms.assetid: e0705b2e-08ea-4ed4-a6df-4c33b934c3dd
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_PORT_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 2e3064a8fc5e1200ab50dce57f519a0165fd1141
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824380"
---
# <a name="oid_gen_port_state"></a>OID\_GEN\_ポート\_の状態


クエリとして、これまでのドライバーでは、OID\_GEN\_ポート\_状態 OID を使用して、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造**のポート番号メンバーに**指定されているポートの現在の状態を取得しています。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS は、この OID およびミニポートドライバーがこの OID クエリを受信しません。

クエリが成功した場合、ndis は NDIS\_STATUS\_SUCCESS を返し、 [**ndis\_ポートの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)構造にポートの状態情報を返します。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_ポート\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)

 

 




