---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: セットとして、NDIS およびそれ以降のドライバーは OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID を使用して、NDIS ポートの現在の状態を設定します。
ms.assetid: 676601c1-2647-4341-9a5c-cee895d2dbf7
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_PORT_AUTHENTICATION_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 193e189fbfd9ac0081f87b864852b7896932d3c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824384"
---
# <a name="oid_gen_port_authentication_parameters"></a>OID\_GEN\_ポート\_認証\_パラメーター


セットとして、NDIS およびそれ以降のドライバーは、OID\_GEN\_ポート\_認証\_パラメーター OID を使用して、NDIS ポートの現在の状態を設定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
(省略可能)。 NDIS ポートの場合は必須です。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS ポートをサポートするミニポートドライバーは、この OID をサポートする必要があります。

ミニポートドライバーでこの OID がサポートされていない場合、ミニポートドライバーは、サポートされていない\_ではなく NDIS\_の状態\_返す必要があります。

ミニポートドライバーでこの OID がサポートされている場合、ドライバーは NDIS\_STATUS\_SUCCESS を返し、 [**ndis\_ポート\_認証\_パラメーターに受信ポートの方向、ポート制御の状態、および認証状態を提供します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)構造体。

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


[**NDIS\_PORT\_認証\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)

 

 




