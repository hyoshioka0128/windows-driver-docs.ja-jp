---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID は、ミニポートアダプターの再起動属性を NDIS ドライバースタックに反映するための一般的な属性を識別します。
ms.assetid: 239993f6-2176-4925-aadc-44e0df66f56b
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MINIPORT_RESTART_ATTRIBUTES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 35ac543cec511a6aa93390fbabe3bcbbe7ec117f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843130"
---
# <a name="oid_gen_miniport_restart_attributes"></a>OID\_GEN\_ミニポート\_再起動\_属性


OID\_GEN\_ミニポート\_再起動\_属性 OID は、ミニポートアダプターの再起動属性を NDIS ドライバースタックに反映するための一般的な属性を識別します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a name="remarks"></a>注釈
-------

Oid\_GEN\_ミニポート\_再起動\_属性 OID は、OID クエリや set 要求の発行には使用されません。

Ndis の**oid**メンバー [ **\_再起動\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)の構造が OID\_GEN\_ミニポート\_再起動\_属性、構造体の**データ**メンバーには NDIS が含まれてい[ **\_一般\_属性構造\_再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)します。

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


[**NDIS\_RESTART\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)

[**NDIS\_\_全般\_属性の再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)

 

 




