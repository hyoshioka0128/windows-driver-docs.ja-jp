---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知を使用して、以前の OID_WWAN_DEVICE_CAPS_EX クエリ要求の完了を MB サービスに通知します。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS_EX ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 3f34c809354df387c1a56bcb8b02df4991d4e40d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842648"
---
# <a name="ndis_status_wwan_device_caps_ex"></a>NDIS\_ステータス\_WWAN\_デバイス\_CAP\_EX


ミニポートドライバーは、 **NDIS の\_ステータス\_wwan\_デバイス\_cap\_ex**通知を使用して、MB サービスに、前の[OID\_WWAN\_デバイス\_cap の完了を通知し\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)クエリ要求。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)構造体を使用します。

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


[OID\_WWAN\_デバイス\_CAP\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)

[**NDIS\_WWAN\_デバイス\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

 

 




