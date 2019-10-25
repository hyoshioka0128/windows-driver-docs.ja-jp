---
title: OID_WWAN_DELETE_MAC
description: OID_WWAN_DELETE_MAC は、NDIS_WWAN_MAC_INFO パラメーターに指定されている NDIS ポートを削除するようにミニポートドライバーに要求します。
ms.assetid: 3C992E0D-132E-4687-B38E-31409E1A9F54
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DELETE_MAC ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: fc43a11868e9efa52bc8aa280dd618cc0233af96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843865"
---
# <a name="oid_wwan_delete_mac"></a>OID\_WWAN\_削除\_MAC


OID\_WWAN\_DELETE\_MAC は、NDIS\_WWAN\_MAC\_INFO パラメーターに指定されている NDIS ポートを削除するようにミニポートドライバーに要求します。 NDIS ポートは、前の手順で作成した[OID\_WWAN\_\_MAC を作成](oid-wwan-create-mac.md)する必要があります。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_STATUS\_を元の要求に戻してから、NDIS\_STATUS を使用して要求を完了\_成功させる必要があります。

クエリ要求はサポートされていません。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、デッドロックを防ぐために、NDIS ポートを非同期的に削除 (非アクティブ化) する要求を処理する必要があります。

OID\_WWAN\_\_既定のポートを削除するために送信された MAC 要求を削除すると、NDIS 状態エラーコード NDIS\_ステータス\_無効な\_ポートで失敗します。

デバイスが非アクティブ化されていない場合は、OID\_WWAN を受信し\_MAC 要求\_削除すると、ポートに関連付けられている PDP コンテキストが非アクティブになります。 これは、突然の削除イベントが発生する可能性があるためです。 このようなときに PDP コンテキストを非アクティブ化すると、モデムとミニポートドライバーが良好な状態であることが保証されます。

ドライバーが突然削除されると、ドライバーはすべての Oid をブロックして取り消します。 これは、[*フィルター\_DETACH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)呼び出しの一部として、WINDOWS が OID\_wwan を使用して呼び出しを送信し、\_mac を削除して\_を削除することを意味する OID\_wwan を除外することを意味します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows の Windows 8.1 以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_\_MAC の作成](oid-wwan-create-mac.md)

 

 




