---
title: NDIS_STATUS_WWAN_SMS_SEND
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SMS_SEND 通知を使用して、OID_WWAN_SMS_SEND を前の送信要求の完了に関する MB サービスに通知します。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_SEND ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0260d8c2314694341098c0960f82d4f163f2ea1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577992"
---
# <a name="ndisstatuswwansmssend"></a>NDIS\_状態\_WWAN\_SMS\_送信


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_SMS\_MB サービスに通知を前の送信要求の完了に関する通知の送信[OID\_WWAN\_SMS\_送信](oid-wwan-sms-send.md)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SMS\_送信\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567944)構造体。

<a name="remarks"></a>コメント
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

[**NDIS\_WWAN\_SMS\_送信\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567944)

 

 




