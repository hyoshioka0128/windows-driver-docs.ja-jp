---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC は、新しい NDIS ポートを作成するようにミニポートドライバーを要求します。
ms.assetid: 4EF98858-86CD-409B-BE41-E57B24158609
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_CREATE_MAC ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f32d589fa027b401361f2a3d7de66b9fa550e0c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843867"
---
# <a name="oid_wwan_create_mac"></a>OID\_WWAN\_\_MAC の作成


OID\_WWAN\_新しい NDIS ポートを作成するために、\_MAC を作成するようにミニポートドライバーを要求します。 追加の PDP コンテキストに対するコンテキストアクティブ化要求は、この新しい NDIS ポートで送信されます。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_\_STATUS を返し、元の要求に必要な\_を示し、その後、 [**ndis\_WWAN\_MAC で要求を完了する必要があり\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)ポートに関連付けられている NDIS ポート番号と MAC アドレスを示す INFO 構造体。

クエリ要求はサポートされていません。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、デッドロックを防ぐために新しい NDIS ポートを非同期的に作成 (アクティブ化) する要求を処理する必要があります。

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


[**NDIS\_WWAN\_MAC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)

[OID\_WWAN\_削除\_MAC](oid-wwan-delete-mac.md)

 

 




