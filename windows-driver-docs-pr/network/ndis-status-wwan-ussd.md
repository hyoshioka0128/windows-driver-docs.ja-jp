---
title: NDIS_STATUS_WWAN_USSD
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_USSD 通知を使用して、NDIS_WWAN_USSD_REQUEST 構造を持つ非構造化補助サービス データ (USSD) 操作のトランザクションの完了の応答を実装します。ミニポート ドライバー NDIS_WWAN_USSD_EVENT 構造体を使用して、USSD イベントの性質を説明するこの通知が不要なイベントを送信できます。
ms.assetid: 6EE1235A-486E-4653-BFAC-6151C795676B
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_USSD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2875075bc7ac93b700573c80277735bc4e417387
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372520"
---
# <a name="ndisstatuswwanussd"></a>NDIS\_状態\_WWAN\_USSD


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_USSD 通知が構造化されていない補助サービス データ (USSD) 操作のトランザクションの完了の応答を実装するために、 [NDIS\_WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)構造体。

ミニポート ドライバーが要請されていないイベントを使用してこの通知を送信できますも、 [NDIS\_WWAN\_USSD\_イベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)USSD イベントの性質を記述する構造体。

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


[NDIS\_WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)

[NDIS\_WWAN\_USSD\_イベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)

 

 




