---
title: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS
description: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS MB デバイスが NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 通知を送信する必要がありますデバイス サービスの一覧に関する情報を設定します。
ms.assetid: 34D38A28-0E81-47B0-9232-F89927DA4B2B
ms.date: 08/08/2017
keywords: -OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a11d2326aa9cc9c17365dff64642485787f9edff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384717"
---
# <a name="oidwwansubscribedeviceserviceevents"></a>OID\_WWAN\_購読\_デバイス\_サービス\_イベント


OID\_WWAN\_購読\_デバイス\_サービス\_MB デバイスが送信する必要がありますのサービスのデバイスの一覧のイベント セットについて[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)通知します。 MB デバイスには、この一覧にない任意のデバイス サービスのイベントを示していませんする必要があります。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription) MB デバイスのイベント サブスクリプションの現在のリストが含まれる状態の通知。

MB デバイス サービス イベント サブスクリプションの一覧の設定を要求する呼び出し元に提供する[ **NDIS\_WWAN\_購読\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)適切な情報、ミニポート ドライバー構造体。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)

[**NDIS\_状態\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)

[**NDIS\_WWAN\_購読\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)

 

 




