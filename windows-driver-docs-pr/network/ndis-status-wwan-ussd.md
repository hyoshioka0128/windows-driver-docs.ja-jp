---
title: NDIS_STATUS_WWAN_USSD
description: ミニポートドライバーは、NDIS_STATUS_WWAN_USSD 通知を使用して、NDIS_WWAN_USSD_REQUEST 構造体を持つ非構造化補助サービスデータ (USSD) 操作に対するトランザクション完了応答を実装します。また、ミニポートドライバーは、NDIS_WWAN_USSD_EVENT 構造体を使用して、USSD イベントの性質を説明するこの通知を使用して、要請されていないイベントを送信することもできます。
ms.assetid: 6EE1235A-486E-4653-BFAC-6151C795676B
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_USSD ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 3a7a30778d728f59e9bc2659a50d4d9ab63a22af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834659"
---
# <a name="ndis_status_wwan_ussd"></a>NDIS\_ステータス\_WWAN\_USSD


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_USSD notification を使用して、 [ndis\_WWAN\_USSD を使用した非構造化補助サービスデータ (USSD) 操作に対するトランザクション完了応答を実装\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)構造体。

また、ミニポートドライバーは、 [NDIS\_WWAN\_USSD\_イベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)構造を使用して、この通知を使用して要請されていないイベントを送信し、USSD イベントの性質を説明することもできます。

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


[NDIS\_WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)

[NDIS\_WWAN\_USSD\_イベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)

 

 




