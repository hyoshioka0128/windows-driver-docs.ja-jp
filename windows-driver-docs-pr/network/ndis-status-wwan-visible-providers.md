---
title: NDIS_STATUS_WWAN_VISIBLE_PROVIDERS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_VISIBLE_PROVIDERS 通知を使用して、OID_WWAN_VISIBLE_PROVIDERS \ 160; クエリ要求の完了を MB サービスに通知します。
ms.assetid: 57e79d45-536a-4ab9-8cc0-0408d722b6f7
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_VISIBLE_PROVIDERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 065d9decdd973639a99a395db3e253a1c3ff54ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834647"
---
# <a name="ndis_status_wwan_visible_providers"></a>NDIS\_ステータス\_WWAN\_表示されている\_プロバイダ


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_表示されている\_プロバイダーの通知を使用して、MB サービスに対して、クエリ要求\_、表示されている[\_プロバイダーに表示](oid-wwan-visible-providers.md)される OID\_の完了を通知します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)の構造が表示されます。

<a name="remarks"></a>注釈
-------

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_表示される\_プロバイダー](oid-wwan-visible-providers.md)

[**NDIS\_WWAN\_表示される\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

 

 




