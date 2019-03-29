---
title: NDIS_STATUS_WWAN_SYS_CAPS_INFO
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_SYS_CAPS_INFO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_SYS_CAPS_INFO 通知を使用します。
ms.assetid: 653A35EC-29BB-458D-B33C-41EF6EF47A6E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SYS_CAPS_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b201eb94dd8f1bd4b45688069f959b1e681001b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580466"
---
# <a name="ndisstatuswwansyscapsinfo"></a>NDIS\_状態\_WWAN\_SYS\_CAP\_情報


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_SYS\_CAP\_情報**MB サービスに以前の完了を通知するために通知[OID\_WWAN\_SYS\_CAP\_情報](https://msdn.microsoft.com/library/windows/hardware/mt799833)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SYS\_CAP\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782410)構造体。

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


[OID\_WWAN\_SYS\_CAP\_情報](https://msdn.microsoft.com/library/windows/hardware/mt799833)

[**NDIS\_WWAN\_SYS\_CAP\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782410)

 

 




