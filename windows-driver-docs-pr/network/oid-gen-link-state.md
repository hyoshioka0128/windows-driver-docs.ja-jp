---
title: OID_GEN_LINK_STATE
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_LINK_STATE OID を使用して、ミニポートアダプターの現在のリンクの状態を判断します。
ms.assetid: 75a30054-8700-4b79-902c-c8382a25c0a2
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_LINK_STATE
ms.localizationpriority: medium
ms.openlocfilehash: 20d1c7b8b2b11fc5e4d51ee3b7fddb6be105e3a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844617"
---
# <a name="oid_gen_link_state"></a>OID\_GEN\_LINK\_の状態


クエリとして、NDIS およびそれ以降のドライバーは OID\_GEN\_リンク\_状態 OID を使用して、ミニポートアダプターの現在のリンクの状態を判断します。 ミニポートドライバーは、 [**NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造のリンク状態を受け取ります。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、初期化中にリンク状態を提供し、状態を示す更新プログラムを提供します。

リンクの状態を指定するには **、MediaConnectState**、 **MediaDuplexState**、 **XmitLinkSpeed**、 **rcvlinkspeed**、 **PauseFunctions**、および**AutoNegotiationFlags**のメンバーを、ミニポートドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡す、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の構造体に設定します。

ミニポートドライバーでこの OID がサポートされていない場合、ドライバーは、サポートされて\_いない\_の NDIS\_状態を返します。 この OID がミニポートドライバーによってサポートされている場合は、 [**NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造の接続状態、双方向の状態、およびリンク速度が返されます。

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


[**NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID\_GEN\_MEDIA\_CONNECT\_STATUS\_EX](oid-gen-media-connect-status-ex.md)

[OID\_GEN\_メディア\_双方向\_状態](oid-gen-media-duplex-state.md)

 

 




