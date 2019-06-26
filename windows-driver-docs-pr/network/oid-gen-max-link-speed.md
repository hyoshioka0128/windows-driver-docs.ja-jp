---
title: OID_GEN_MAX_LINK_SPEED
description: クエリとして NDIS および上にあるドライバーを使用して OID_GEN_MAX_LINK_SPEED OID 最大送信をサポートおよびミニポート アダプターのリンク速度を受信します。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -OID_GEN_MAX_LINK_SPEED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1c23d18623989c565594fdefb44f25d452ab46b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369062"
---
# <a name="oidgenmaxlinkspeed"></a>OID\_GEN\_最大\_リンク\_速度


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_最大\_リンク\_ミニポート アダプターのリンク速度の送受信をサポートされている最大を決定する速度の OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、初期化中に最大リンク速度を提供します。

最大のリンク速度を指定するには、設定、 **MaxXmitLinkSpeed**と**MaxRcvLinkSpeed**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。 ミニポート ドライバーがこの OID をサポートしていない場合、ドライバーは NDIS を返す必要があります\_状態\_いない\_サポートされています。 ミニポート ドライバーでは、この OID をサポートする場合の最大数のリンク速度が返されます、 [ **NDIS\_リンク\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_speed)構造体。

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


[**NDIS\_リンク\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_speed)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

 

 




