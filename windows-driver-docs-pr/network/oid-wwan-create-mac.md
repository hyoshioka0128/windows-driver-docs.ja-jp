---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC では、新しい NDIS ポートを作成するミニポート ドライバーを要求します。
ms.assetid: 4EF98858-86CD-409B-BE41-E57B24158609
ms.date: 08/08/2017
keywords: -OID_WWAN_CREATE_MAC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f47777cb33098ad3fc733c2158d8e2446bf6f553
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362855"
---
# <a name="oidwwancreatemac"></a>OID\_WWAN\_作成\_MAC


OID\_WWAN\_作成\_MAC は、新しい NDIS ポートを作成するミニポート ドライバーを要求します。 追加の PDP コンテキストのコンテキストのアクティブ化要求は、この新しい NDIS ポートで送信されます。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求と後で使用して要求を完了するには、必要な作業、 [ **NDIS\_WWAN\_MAC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)ポートに関連付けられているポート番号の NDIS と MAC アドレスを示す構造体。

クエリ要求はサポートされていません。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーを作成する要求を処理する必要があります (アクティブ化) のデッドロックを防ぐために非同期的に新しい NDIS ポート。

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
<td><p>Windows 8.1 と Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_MAC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)

[OID\_WWAN\_削除\_MAC](oid-wwan-delete-mac.md)

 

 




