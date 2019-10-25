---
title: OID_GEN_LINK_SPEED_EX
description: クエリとして、OID_GEN_LINK_SPEED_EX OID はインターフェイスの送信および受信リンク速度を提供します。 バージョン情報 Windows Vista および laterSupported。 NDIS 6.0 以降のミニポートの場合は要求されません。 NDIS インターフェイスプロバイダーのみ。
ms.assetid: 86cc281b-3898-484c-9418-4408a45ebe71
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_LINK_SPEED_EX ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e68913f9bf015d230b0eb0a8b0c6d6b14a518769
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844619"
---
# <a name="oid_gen_link_speed_ex"></a>OID\_GEN\_リンク\_速度\_EX


クエリとして、OID\_GEN\_リンク\_速度\_EX では、インターフェイスの送信および受信リンク速度が提供されます。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>注釈
-------

NDIS は、この OID を使用して、 [ndis ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーのリンク速度を照会します。 この OID を OID 要求としてサポートする必要があるのは、NDIS インターフェイスプロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートしません。

この OID は、 [**NDIS\_リンク\_SPEED**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)構造のリンク速度を返します。

ミニポートドライバーは、初期化中にリンク速度を提供し、ステータスを示すリンク速度を更新します。

ミニポートドライバーでリンク速度を指定するには、ミニポートドライバーによって渡される[**NDIS\_ミニポート\_アダプター\_GENERAL\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**XmitLinkSpeed**および**rcvlinkspeed**メンバーを設定します。[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数。

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


[**NDIS\_リンクの\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




