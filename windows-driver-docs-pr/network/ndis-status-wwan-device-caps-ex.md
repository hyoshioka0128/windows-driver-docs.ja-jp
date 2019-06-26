---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_DEVICE_CAPS_EX クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知を使用します。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a27e48a081a967e87c3f375cacbed14e1b8a0f6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375177"
---
# <a name="ndisstatuswwandevicecapsex"></a>NDIS\_状態\_WWAN\_デバイス\_CAP\_例


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_デバイス\_CAP\_EX** MB サービスに以前の完了を通知するために通知[OID\_WWAN\_デバイス\_CAP\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_CAP\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)構造体。

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
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_CAP\_例](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)

[**NDIS\_WWAN\_デバイス\_CAP\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

 

 




