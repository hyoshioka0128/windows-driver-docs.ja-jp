---
title: NDIS_STATUS_WWAN_VISIBLE_PROVIDERS
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_VISIBLE_PROVIDERS 通知を使用して、OID_WWAN_VISIBLE_PROVIDERS の完了に関する MB サービスに通知する \ 160; クエリ要求。
ms.assetid: 57e79d45-536a-4ab9-8cc0-0408d722b6f7
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_VISIBLE_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5117503621e9d52943ed887c385e0b145330a233
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384387"
---
# <a name="ndisstatuswwanvisibleproviders"></a>NDIS\_状態\_WWAN\_VISIBLE\_プロバイダー


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_VISIBLE\_MB サービスに通知の完了に関する通知をプロバイダー [OID\_WWAN\_VISIBLE\_プロバイダー](oid-wwan-visible-providers.md) 要求のクエリを実行します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_VISIBLE\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)構造体。

<a name="remarks"></a>注釈
-------

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_VISIBLE\_プロバイダー](oid-wwan-visible-providers.md)

[**NDIS\_WWAN\_VISIBLE\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

 

 




