---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_CAPS 通知を使用して OID_WWAN_DEVICE_CAPS クエリ要求に応答します。 ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。この通知では、NDIS_WWAN_DEVICE_CAPS 構造体が使用されます。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e98e2ed9a5f3ab6dd2f70caad0380595098ba277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842632"
---
# <a name="ndis_status_wwan_device_caps"></a>NDIS\_ステータス\_WWAN\_デバイス\_CAP


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_CAP 通知を使用して、 [OID\_wwan\_デバイス\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリ要求に応答します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_DEVICE\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体を使用します。

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


[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)

[**NDIS\_WWAN\_デバイス\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

 

 




