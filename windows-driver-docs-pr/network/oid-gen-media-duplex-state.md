---
title: OID_GEN_MEDIA_DUPLEX_STATE
description: クエリとしては、OID_GEN_MEDIA_DUPLEX_STATE OID は、インターフェイスの双方向の状態を返します。 バージョン情報の Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: 63776227-dc48-4506-888f-c4b944837c4c
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_DUPLEX_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dfcd9b326b95571fa667368358d8db7bb987b08f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369023"
---
# <a name="oidgenmediaduplexstate"></a>OID\_GEN\_メディア\_双方向\_状態


クエリ、OID として\_GEN\_メディア\_双方向\_状態 OID がインターフェイスの双方向の状態を返します。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

NDIS では、この OID を使用して、双方向の状態を照会、[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー。 のみ NDIS インターフェイス プロバイダー、およびしたがってミニポート ドライバーではないまたはフィルター ドライバー、する必要がありますサポートこの OID OID 要求として。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、値のいずれかで指定できます、 [ **NET\_場合\_メディア\_双方向\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)列挙体。

ミニポート ドライバーでは、初期化中に、メディアの状態の双方向を指定し、状態インジケーターの更新プログラムを提供します。

ミニポート ドライバーでは、双方向の状態を指定するには、設定、 **MediaDuplexState**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。

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


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NET\_IF\_MEDIA\_DUPLEX\_STATE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




