---
title: NDIS_STATUS_WWAN_SMS_DELETE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SMS_DELETE 通知を使用して、OID_WWAN_SMS_DELETE を介して以前削除要求の完了に関する MB サービスに通知します。
ms.assetid: 0083dcd9-4e18-4582-993a-c4402cb552de
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 317407fb348d5cda72f5ad97ca597458e45023d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386859"
---
# <a name="ndisstatuswwansmsdelete"></a>NDIS\_状態\_WWAN\_SMS\_削除


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスを介して以前削除要求の完了に通知するために削除通知[OID\_WWAN\_SMS\_削除](oid-wwan-sms-delete.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_削除\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)構造体。

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


[OID\_WWAN\_SMS\_削除](oid-wwan-sms-delete.md)

[**NDIS\_WWAN\_SMS\_削除\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)

 

 




