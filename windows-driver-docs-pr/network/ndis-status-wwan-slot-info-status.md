---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_SLOT_INFO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_SLOT_INFO 通知を使用します。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SLOT_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0ca1d607ab0e4ca65d5f828b7ac6419f3d16395e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386862"
---
# <a name="ndisstatuswwanslotinfo"></a>NDIS\_STATUS\_WWAN\_SLOT\_INFO


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_スロット\_情報**MB サービスに前回の完了を通知するために通知[OID\_WWAN\_スロット\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)クエリ要求。

ミニポート ドライバーに送信できる、 **NDIS\_状態\_WWAN\_スロット\_情報**スロット/カードの状態が変更されたときに、要請していないイベントとして通知します。

この通知を使用して、 [ **NDIS\_WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)構造体。

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
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_SLOT\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)

[**NDIS\_WWAN\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

 

 




