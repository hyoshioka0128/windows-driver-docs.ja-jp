---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: ミニポート ドライバーでは、OID_WWAN_DEVICE_CAPS クエリ要求に応答する NDIS_STATUS_WWAN_DEVICE_CAPS 通知を使用します。 ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。この通知は、NDIS_WWAN_DEVICE_CAPS 構造体を使用します。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d841f33ded4396c3376390790be313a93ee2250c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382639"
---
# <a name="ndisstatuswwandevicecaps"></a>NDIS\_状態\_WWAN\_デバイス\_キャップ


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_CAP 通知に応答する[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体。

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


[OID\_WWAN\_デバイス\_キャップ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)

[**NDIS\_WWAN\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

 

 




