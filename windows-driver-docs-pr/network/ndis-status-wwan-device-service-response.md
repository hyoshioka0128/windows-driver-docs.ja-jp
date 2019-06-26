---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
description: ミニポート ドライバーでは、OID_WWAN_DEVICE_SERVICE_COMMAND のトランザクションの完了の応答を実装するために、NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE を示す値を使用します。NDIS_WWAN_DEVICE_SERVICE_RESPONSE 構造体。
ms.assetid: 2817EAFA-7A9A-4DC1-B2B7-31E1F4E5E331
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dab0f6c21b96673cd6b928e44eb17eba20c1007e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385509"
---
# <a name="ndisstatuswwandeviceserviceresponse"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_応答


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_のトランザクションの完了の応答を実装するために応答を示す値[OID\_WWAN\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_応答**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)構造体。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)

[**NDIS\_WWAN\_デバイス\_サービス\_応答**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)

 

 




