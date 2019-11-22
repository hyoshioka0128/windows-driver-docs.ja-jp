---
title: OID_GEN_MEDIA_DUPLEX_STATE
description: クエリとして OID_GEN_MEDIA_DUPLEX_STATE OID は、インターフェイスの双方向の状態を返します。 バージョン情報 Windows Vista および laterSupported。 NDIS 6.0 以降のミニポートの場合は要求されません。 NDIS インターフェイスプロバイダーのみ。
ms.assetid: 63776227-dc48-4506-888f-c4b944837c4c
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_MEDIA_DUPLEX_STATE
ms.localizationpriority: medium
ms.openlocfilehash: 30f2bfa421e52ef3091fec615b1fec89a82468d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834149"
---
# <a name="oid_gen_media_duplex_state"></a>OID\_GEN\_メディア\_双方向\_状態


クエリとして、OID\_GEN\_MEDIA\_DUPLEX\_状態 OID は、インターフェイスの双方向の状態を返します。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>注釈
-------

NDIS は、この OID を使用して、 [ndis ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーの双方向の状態を照会します。 この OID を OID 要求としてサポートする必要があるのは、NDIS インターフェイスプロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートしません。

クエリが成功した場合、インターフェイスプロバイダーは NDIS\_STATUS\_SUCCESS を返します。 [ **\_メディア\_双方向\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)列挙型の場合、クエリの結果は NET\_の値のいずれかになります。

ミニポートドライバーは、初期化中にメディア双方向の状態を提供し、状態を示す更新プログラムを提供します。

ミニポートドライバーで双方向の状態を指定するには、ミニポートドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡す、 [**NDIS\_ミニポート\_アダプター\_GENERAL\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**MediaDuplexState**メンバーを設定します。

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

[ **\_メディア\_双方向\_状態の場合、NET\_** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




