---
title: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS
description: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS は、MB デバイスが NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 通知を送信する必要があるデバイスサービスの一覧に関する情報を設定します。
ms.assetid: 34D38A28-0E81-47B0-9232-F89927DA4B2B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 12afb51891a3b42e32b9ab1ccd20deb32261cb9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843779"
---
# <a name="oid_wwan_subscribe_device_service_events"></a>OID\_WWAN\_サブスクライブ\_デバイス\_サービス\_イベント


OID\_WWAN\_サブスクライブ\_デバイス\_サービス\_イベントのデバイスサービスの一覧に関する情報を設定します。この情報を使用して、MB デバイスが[**NDIS\_STATUS\_デバイス\_サービスに送信する必要があり\_11_ イベント**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)通知。 MB デバイスは、この一覧に含まれていないデバイスサービスのイベントを示すことはできません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)MB デバイス上のイベントサブスクリプションの現在の一覧を含むサービス\_サブスクリプションの状態通知。

MB デバイスサービスイベントサブスクリプションリストを設定するように要求された呼び出し元は、 [**NDIS\_WWAN\_、\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)構造をミニポートドライバーに登録して、適切な情報を提供します。

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
<td><p>バージョン: Windows 8 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ステータス\_WWAN\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)

[**NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)

[**NDIS\_WWAN\_サブスクライブ\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)

 

 




