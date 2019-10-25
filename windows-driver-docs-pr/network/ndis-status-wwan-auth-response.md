---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_AUTH_RESPONSE 通知を使用して、OID_WWAN_AUTH_CHALLENGE クエリ要求を使用して発行された前回のチャレンジ要求から受信したチャレンジ応答を MB サービスに通知します。NDIS_WWAN_AUTH_RESPONSE 構造体。
ms.assetid: 24831764-4F6D-481B-A440-4F9CAE1F7501
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_AUTH_RESPONSE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 4697b98626621dbdce16eb744a501e11e17ea8ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844653"
---
# <a name="ndis_status_wwan_auth_response"></a>NDIS\_ステータス\_WWAN\_認証\_応答


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_AUTH\_応答通知を使用して、 [OID\_wwan\_auth を使用して発行された前回のチャレンジ要求から受信したチャレンジ応答を MB サービスに通知\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)クエリ要求。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この NDIS 状態通知では、 [ndis\_WWAN\_AUTH\_RESPONSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)構造体を使用します。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_認証\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)

[NDIS\_WWAN\_認証\_応答](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)

 

 




