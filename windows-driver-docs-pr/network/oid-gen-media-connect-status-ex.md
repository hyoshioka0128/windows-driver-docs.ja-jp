---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: クエリとしては、OID_GEN_MEDIA_CONNECT_STATUS_EX OID は、インターフェイスの接続の状態を返します。 Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_CONNECT_STATUS_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d317fda5c069f452ae466f25f42ef41ff8af4126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369036"
---
# <a name="oidgenmediaconnectstatusex"></a>OID\_GEN\_メディア\_CONNECT\_状態\_例


クエリ、OID として\_GEN\_メディア\_CONNECT\_状態\_EX OID がインターフェイスの接続状態を返します。

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

NDIS の接続の状態を照会するこの OID を使用して、[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー。 のみ NDIS インターフェイス プロバイダー、およびしたがってミニポート ドライバーではないまたはフィルター ドライバー、する必要がありますサポートこの OID OID 要求として。

クエリが成功すると、インターフェイス プロバイダーを返します NDIS\_状態\_成功して、クエリの結果は、値のいずれかで指定できます、 [ **NET\_場合\_メディア\_CONNECT\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)列挙体。

ミニポート ドライバー供給メディアは、初期化中に状態を接続し、状態インジケーターの更新プログラムを提供します。

ミニポート ドライバーで接続状態を指定するには、設定、 **MediaConnectState**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。

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


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

[**NET\_場合\_メディア\_CONNECT\_状態**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)

[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




