---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知を使用して、OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS セット要求への応答でデバイスのサービス サブスクリプションに関する MB サービスに通知します。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 構造体。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: efbe036efb411c9649bdecb12166cb967b67453f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366605"
---
# <a name="ndisstatuswwandeviceservicesubscription"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_サブスクリプション


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_MB サービスへの応答内のサービス サブスクリプションにデバイスに通知するためにサブスクリプションの通知、 [OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)セットの要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

このを示す値を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)構造体。

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


[OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)

[**NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)

 

 




