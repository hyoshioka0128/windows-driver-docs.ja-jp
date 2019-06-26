---
title: NDIS_STATUS_WWAN_SYS_CAPS_INFO
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_SYS_CAPS_INFO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_SYS_CAPS_INFO 通知を使用します。
ms.assetid: 653A35EC-29BB-458D-B33C-41EF6EF47A6E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SYS_CAPS_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: df408cd78839bce928418021e44855ec5c3a6103
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372516"
---
# <a name="ndisstatuswwansyscapsinfo"></a>NDIS\_状態\_WWAN\_SYS\_CAP\_情報


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_SYS\_CAP\_情報**MB サービスに以前の完了を通知するために通知[OID\_WWAN\_SYS\_CAP\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)構造体。

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


[OID\_WWAN\_SYS\_CAP\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

 

 




