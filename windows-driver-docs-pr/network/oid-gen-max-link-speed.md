---
title: OID_GEN_MAX_LINK_SPEED
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_MAX_LINK_SPEED OID を使用して、ミニポートアダプターの最大の送信および受信リンク速度を決定します。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MAX_LINK_SPEED ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a0a6b8c7aebdddbd8617acbe05b52f7c367ff5ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843068"
---
# <a name="oid_gen_max_link_speed"></a>OID\_GEN\_最大\_リンク\_速度


クエリとして、NDIS およびそれ以降のドライバーは OID\_GEN\_MAX\_リンク\_速度 OID を使用して、ミニポートアダプターのサポートされている最大送信速度と受信リンク速度を決定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、初期化中に最大リンク速度を提供します。

リンク速度の最大値を指定するには、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**MaxXmitLinkSpeed**および**maxrcvlinkspeed**メンバーを設定します。これは、ミニポートドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数。 ミニポートドライバーでこの OID がサポートされていない場合、ドライバーは、サポートされて\_いない\_の NDIS\_状態を返します。 ミニポートドライバーでこの OID がサポートされている場合は、 [**NDIS\_リンクの\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)構造の最大リンク速度が返されます。

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

 

 




