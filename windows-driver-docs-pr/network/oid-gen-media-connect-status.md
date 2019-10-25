---
title: OID_GEN_MEDIA_CONNECT_STATUS
description: クエリとして、OID_GEN_MEDIA_CONNECT_STATUS OID はネットワーク上の NIC の接続状態を要求します。
ms.assetid: 3ed26e62-a285-4b78-91c6-7c3cc0963570
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MEDIA_CONNECT_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 417fed779300e0c485d2487f9ca220d130d06e9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834157"
---
# <a name="oid_gen_media_connect_status"></a>OID\_GEN\_メディア\_接続\_の状態


クエリとして、OID\_GEN\_MEDIA\_CONNECT\_STATUS OID は、ネットワーク上の NIC の接続状態を要求します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a name="remarks"></a>注釈
-------

Ndis は、この OID を NDIS 6.0 以降のミニポートドライバー用に処理します。

OID\_GEN\_MEDIA\_CONNECT\_STATUS OID は、次のシステム定義の値のいずれかとしてネットワーク上の NIC の接続状態を要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

ネットワーク接続が失われたことがミニポートドライバーによって検知された場合、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)または[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)関数も、NDIS\_STATUS\_MEDIA\_DISCONNECT (ndis 5.1 の場合) または ndis で呼び出される必要があります。ステータス\_MediaConnectStateDisconnected に\_状態をリンクするには、プロパティ (NDIS 6.x の場合) を使用します。\_ 接続が復元されたら、NDIS\_STATUS\_MEDIA\_CONNECT (NDIS 5.1 の場合) または NDIS\_ステータス\_リンク\_状態を MediaConnectStateConnected として、 **Ndism (Co) IndicateStatus**を呼び出す必要があります。MediaConnectState プロパティ (NDIS 6.x の場合)。

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


[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




