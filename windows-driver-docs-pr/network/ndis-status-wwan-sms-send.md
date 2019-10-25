---
title: NDIS_STATUS_WWAN_SMS_SEND
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SMS_SEND 通知を使用して、OID_WWAN_SMS_SEND による前の送信要求の完了を MB サービスに通知します。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SMS_SEND ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 56a8a7cdc44a7d6504202a0214b809b7cde9d486
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844631"
---
# <a name="ndis_status_wwan_sms_send"></a>NDIS\_ステータス\_WWAN\_SMS\_送信


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SMS\_送信通知を使用して、MB サービスに対して、OID\_[wwan\_sms\_send](oid-wwan-sms-send.md)による前回の送信要求の完了を通知します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_SMS\_送信\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)構造を使用します。

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


[OID\_WWAN\_SMS\_送信](oid-wwan-sms-send.md)

[**NDIS\_WWAN\_SMS\_送信\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)

 

 




