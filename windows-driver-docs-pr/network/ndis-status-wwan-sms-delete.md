---
title: NDIS_STATUS_WWAN_SMS_DELETE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SMS_DELETE 通知を使用して、OID_WWAN_SMS_DELETE による以前の削除要求の完了を MB サービスに通知します。
ms.assetid: 0083dcd9-4e18-4582-993a-c4402cb552de
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SMS_DELETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 996f9b9b4acde47d13f5403f80d1ffd236bed17b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844633"
---
# <a name="ndis_status_wwan_sms_delete"></a>NDIS\_ステータス\_WWAN\_SMS\_削除


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_SMS\_削除通知を使用して、MB サービスに対して、OID\_[WWAN\_sms\_delete](oid-wwan-sms-delete.md)による以前の削除要求の完了を通知します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_SMS\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)構造の削除を使用します。

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


[OID\_WWAN\_SMS\_削除](oid-wwan-sms-delete.md)

[**NDIS\_WWAN\_SMS\_削除\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)

 

 




