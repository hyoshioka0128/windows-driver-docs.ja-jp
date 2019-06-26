---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_AUTH_RESPONSE 通知を使用して、OID_WWAN_AUTH_CHALLENGE のクエリ要求を使用して発行前チャレンジの要求から受信したチャレンジ応答の MB サービスに通知します。NDIS_WWAN_AUTH_RESPONSE 構造体。
ms.assetid: 24831764-4F6D-481B-A440-4F9CAE1F7501
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_AUTH_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c349fad7075286e8ab2c144b6e0d9801d3a7131a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382664"
---
# <a name="ndisstatuswwanauthresponse"></a>NDIS\_状態\_WWAN\_AUTH\_応答


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_AUTH\_MB のサービスを使用して発行前チャレンジの要求から受信したチャレンジ応答の通知に応答の通知、 [OID\_WWAN\_AUTH\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)クエリ要求。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この NDIS 状態の通知を使用して、 [NDIS\_WWAN\_AUTH\_応答](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)構造体。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_AUTH\_チャレンジ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)

[NDIS\_WWAN\_AUTH\_RESPONSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)

 

 




