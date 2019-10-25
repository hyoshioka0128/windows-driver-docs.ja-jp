---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION を使用して、OID_WWAN_DEVICE_SERVICE_SESSION によって送信されたデバイスサービスセッション状態の変更の完了を報告します。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 構造体。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 7600f959a03639ea01629c14c4637467a057e122
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843035"
---
# <a name="ndis_status_wwan_device_service_session"></a>\_デバイス\_サービス\_セッションの NDIS\_ステータス\_。


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッションの表示を使用して、 [OID\_WWAN\_デバイスによって送信されたデバイスサービスセッション状態の変更の完了を報告し\_サービス\_セッション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)構造を使用します。

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


[OID\_WWAN\_デバイス\_サービス\_セッション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)

[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)

 

 




