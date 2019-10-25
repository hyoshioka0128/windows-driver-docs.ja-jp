---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 表示を使用して、デバイスサービスの変更を MB サービスに通知します。NDIS_WWAN_DEVICE_SERVICE_EVENT 構造体。
ms.assetid: 2414F63D-756F-4057-974C-A363CEB6399B
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 20e71f3fbe7a987ca122fb550beef15bfe329dd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842647"
---
# <a name="ndis_status_wwan_device_service_event"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_イベント


ミニポートドライバーは、デバイスサービスの変更を MB サービスに通知するために、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_イベント通知を使用します。

ミニポートドライバーは、この通知のみを使用して、要請されていないイベントを送信できます。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)構造を使用します。

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


[**NDIS\_WWAN\_デバイス\_サービス\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_event)

 

 




