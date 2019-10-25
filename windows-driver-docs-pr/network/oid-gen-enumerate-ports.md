---
title: OID_GEN_ENUMERATE_PORTS
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_ENUMERATE_PORTS OID を使用して、基になるミニポートアダプターに関連付けられているアクティブな NDIS ポートの特性を判断します。
ms.assetid: 42a12a05-e360-4493-b037-d3a63906a132
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_ENUMERATE_PORTS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 55dadb183b11c8574e1d46b145bf34e27d79facf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837984"
---
# <a name="oid_gen_enumerate_ports"></a>OID\_GEN\_\_ポートの列挙


クエリとして、NDIS およびそれ以降のドライバーは、OID\_GEN\_使用して\_ポート OID を列挙し、基になるミニポートアダプターに関連付けられているアクティブな NDIS ポートの特性を判断します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS は、この OID およびミニポートドライバーがこの OID クエリを受信しません。

クエリが成功した場合、ndis は NDIS\_STATUS\_SUCCESS を返し、 [**ndis\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)構造にクエリの結果を提供します。 NDIS\_PORT\_ARRAY の**Numberofports**メンバーには、ミニポートアダプターに関連付けられているアクティブなポートの数が含まれています。 NDIS\_PORT\_ARRAY の**Ports**メンバーには、 [**ndis\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造へのポインターの一覧が含まれています。 各 NDIS\_PORT\_特性構造は、単一の NDIDS ポートの特性を定義します。

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


[**NDIS\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)

[**NDIS\_ポート\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)

 

 




