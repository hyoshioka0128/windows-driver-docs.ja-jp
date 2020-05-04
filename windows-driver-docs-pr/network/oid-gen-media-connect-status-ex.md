---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: クエリとして OID_GEN_MEDIA_CONNECT_STATUS_EX OID は、インターフェイスの接続状態を返します。 Windows Vista と laterSupported。 NDIS 6.0 以降のミニポートの場合は要求されません。 NDIS インターフェイスプロバイダーのみ。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_MEDIA_CONNECT_STATUS_EX
ms.localizationpriority: medium
ms.openlocfilehash: 29022ff224cf18cf0c8964710b678c87aae42d3f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82104608"
---
# <a name="oid_gen_media_connect_status_ex"></a>OID\_生成\_メディア\_接続\_の\_状態 (例)


クエリとして、OID\_GEN\_MEDIA\_CONNECT\_STATUS\_EX oid は、インターフェイスの接続状態を返します。

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>解説
-------

NDIS は、この OID を使用して、 [ndis ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーの接続状態を照会します。 この OID を OID 要求としてサポートする必要があるのは、NDIS インターフェイスプロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートしません。

クエリが成功した場合、インターフェイスプロバイダーは\_NDIS\_ステータス SUCCESS を返し、クエリの結果は[**NET\_IF\_\_MEDIA CONNECT\_状態**](https://docs.microsoft.com/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state)列挙のいずれかの値になります。

ミニポートドライバーは、初期化中にメディア接続状態を提供し、状態を示す更新プログラムを提供します。

ミニポートドライバーで接続状態を指定するには、ミニポートドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡す[**NDIS\_ミニポート\_アダプター\_の GENERAL\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**MediaConnectState**メンバーを設定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ミニ\_ポート\_アダプター\_の全般属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**メディア\_\_接続\_\_状態の場合は NET**](https://docs.microsoft.com/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state)

[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




