---
title: NDIS_STATUS_WWAN_SMS_SEND
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SMS_SEND 通知を使用して、OID_WWAN_SMS_SEND を前の送信要求の完了に関する MB サービスに通知します。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_SEND ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 06ca8f6dadddb7e7f818ab67a06e1786e92ba2de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372532"
---
# <a name="ndisstatuswwansmssend"></a>NDIS\_状態\_WWAN\_SMS\_送信


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスに通知を前の送信要求の完了に関する通知の送信[OID\_WWAN\_SMS\_送信](oid-wwan-sms-send.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_送信\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)構造体。

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


[OID\_WWAN\_SMS\_送信](oid-wwan-sms-send.md)

[**NDIS\_WWAN\_SMS\_送信\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)

 

 




