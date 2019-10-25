---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SLOT_INFO 通知を使用して、以前の OID_WWAN_SLOT_INFO クエリ要求の完了を MB サービスに通知します。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SLOT_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ce116993d1b9a7ad29896672edac33c87edfcb2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844639"
---
# <a name="ndis_status_wwan_slot_info"></a>NDIS\_ステータス\_WWAN\_スロット\_情報


ミニポートドライバーは、 **NDIS\_ステータス\_wwan\_スロット\_情報**通知を使用して、以前の[OID\_WWAN\_スロット\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)クエリ要求の完了を MB サービスに通知します。

ミニポートドライバーは、スロット/カードの状態が変化したときに、要請されていないイベントとして、 **NDIS\_ステータス\_WWAN\_スロット\_情報**通知を送信できます。

この通知では、 [**NDIS\_WWAN\_スロット\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)構造体を使用します。

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
<td><p>Windows 10 バージョン1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_スロット\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)

[**NDIS\_WWAN\_スロット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

 

 




