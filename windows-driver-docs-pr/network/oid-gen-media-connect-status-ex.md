---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: クエリとして、OID_GEN_MEDIA_CONNECT_STATUS_EX OID はインターフェイスの接続状態を返します。 Windows Vista と laterSupported。 NDIS 6.0 以降のミニポートの場合は要求されません。 NDIS インターフェイスプロバイダーのみ。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MEDIA_CONNECT_STATUS_EX ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 681148b4da1a7d354b9b17ab53c47ce5e4a694db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845059"
---
# <a name="oid_gen_media_connect_status_ex"></a>OID\_GEN\_MEDIA\_CONNECT\_STATUS\_EX


クエリとして、OID\_GEN\_MEDIA\_CONNECT\_STATUS\_EX OID はインターフェイスの接続状態を返します。

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>注釈
-------

NDIS は、この OID を使用して、 [ndis ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーの接続状態を照会します。 この OID を OID 要求としてサポートする必要があるのは、NDIS インターフェイスプロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートしません。

クエリが成功した場合、インターフェイスプロバイダーは NDIS\_STATUS\_SUCCESS を返し、クエリの結果は NET\_の値のいずれかになります ( [ **\_メディア\_接続\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)の列挙)。

ミニポートドライバーは、初期化中にメディア接続状態を提供し、状態を示す更新プログラムを提供します。

ミニポートドライバーで接続状態を指定するには、 [**NDIS\_ミニポート\_\_\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の MediaConnectState メンバーを設定し、ミニポートドライバー[**がNdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数。

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


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[ **\_メディア\_接続\_状態の場合、NET\_** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)

[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




