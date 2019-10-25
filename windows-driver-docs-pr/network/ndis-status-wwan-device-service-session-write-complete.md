---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 通知を使用して、デバイスサービスセッションでの書き込み操作の状態を報告します。NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 構造体。
ms.assetid: 39C0FE62-E262-4D7D-8A93-6C31431AF846
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9891afecc7b8b91f442c924ee0547366ee0811b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843038"
---
# <a name="ndis_status_wwan_device_service_session_write_complete"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了


ミニポートドライバーは、デバイスサービスセッションでの書き込み操作の状態を報告するために、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了通知を使用します。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_セッション\_\_完全な**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete)構造の書き込みを使用します。

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


[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete)

 

 




