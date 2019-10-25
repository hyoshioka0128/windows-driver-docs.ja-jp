---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 通知を使用して、開いているデバイスサービスセッションからデータを受信したことを MB サービスに通知します。NDIS_WWAN_DEVICE_SERVICE_SESSION_READ 構造体。
ms.assetid: 680C15DA-B37C-4A7C-B7BE-B13B3B050EC3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e7367ea39d88d8340dfb54775cad6a2de39bd50c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838890"
---
# <a name="ndis_status_wwan_device_service_session_read"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッション\_読み取り


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッション\_読み取り通知を使用して、開いているデバイスサービスセッションからデータが受信されたことを MB サービスに通知します。

ミニポートドライバーは、この通知のみを使用して、要請されていないイベントを送信できます。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_セッション\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)構造を使用します。

<a name="requirements"></a>前提条件
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
<td><p>ヘッダー</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)

 

 




