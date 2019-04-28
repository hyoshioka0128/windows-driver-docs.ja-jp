---
title: NDIS_STATUS_WWAN_SMS_DELETE
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SMS_DELETE 通知を使用して、OID_WWAN_SMS_DELETE を介して以前削除要求の完了に関する MB サービスに通知します。
ms.assetid: 0083dcd9-4e18-4582-993a-c4402cb552de
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7bead5976d32c229c9527615f0395d25fe9a5bee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372187"
---
# <a name="ndisstatuswwansmsdelete"></a>NDIS\_状態\_WWAN\_SMS\_削除


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスを介して以前削除要求の完了に通知するために削除通知[OID\_WWAN\_SMS\_削除](oid-wwan-sms-delete.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_削除\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567940)構造体。

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

[**NDIS\_WWAN\_SMS\_削除\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567940)

 

 




