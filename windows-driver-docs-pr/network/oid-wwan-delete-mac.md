---
title: OID_WWAN_DELETE_MAC
description: OID_WWAN_DELETE_MAC は、NDIS_WWAN_MAC_INFO パラメーターで指定された NDIS ポートを削除するミニポート ドライバーを要求します。
ms.assetid: 3C992E0D-132E-4687-B38E-31409E1A9F54
ms.date: 08/08/2017
keywords: -OID_WWAN_DELETE_MAC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ae5d5e1f04ffef07ef6d6b37083f52caa912c5e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362850"
---
# <a name="oidwwandeletemac"></a>OID\_WWAN\_削除\_MAC


OID\_WWAN\_削除\_MAC 要求、NDIS で指定された NDIS ポートを削除するミニポート ドライバー\_WWAN\_MAC\_INFO パラメーター。 NDIS ポートが作成を使用して[OID\_WWAN\_作成\_MAC](oid-wwan-create-mac.md)します。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_元の要求と後で NDIS を使用して要求を完了する保留\_状態\_成功します。

クエリ要求はサポートされていません。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーを削除する要求を処理する必要があります (非アクティブ化) のデッドロックを防ぐために非同期的に NDIS ポート。

OID\_WWAN\_削除\_NDIS 状態エラー コード NDIS 削除の既定のポートに送信された MAC 要求は失敗\_状態\_無効な\_ポート。

OID を受け取ると\_WWAN\_削除\_ミニポート ドライバーを非アクティブ化、ポートに関連付けられた PDP コンテキストがない既に非アクティブの場合、MAC を要求します。 これは、突然の削除イベントが発生する可能性があるためにです。 このような時に PDP コンテキストを非アクティブ化では、モデムとミニポート ドライバーを正常な状態で維持することが確認されます。

ときに、ドライバーは、突然削除すると、ドライバーのブロックを受信し、さらにすべての Oid を取り消します。 つまり、ドライバーが除外 OID\_WWAN\_削除\_Windows OID で呼び出しを送信する場合でも MAC\_WWAN\_削除\_MAC の一部として、 [ *フィルター\_デタッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)呼び出します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 と Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_作成\_MAC](oid-wwan-create-mac.md)

 

 




