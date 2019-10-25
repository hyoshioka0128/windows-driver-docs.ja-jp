---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知を使用して、OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS set 要求への応答としてデバイスサービスサブスクリプションに関する情報を MB サービスに通知します。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 構造体。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 038ddc7e5bbff54eadf84cfc4d0aa4743841782b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843033"
---
# <a name="ndis_status_wwan_device_service_subscription"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サブスクリプション


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サブスクリプション通知を使用して、デバイスサービスサブスクリプションに関する情報を MB サービスに通知します。これは、 [OID\_WWAN\_サブスクライブに応答して\_DEVICE\_SERVICE\_EVENTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events) set request。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この表示では、 [**NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)構造を使用します。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_サブスクライブ\_デバイス\_サービス\_イベント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)

[**NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)

 

 




