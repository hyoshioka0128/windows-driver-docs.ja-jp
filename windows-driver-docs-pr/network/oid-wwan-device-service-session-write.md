---
title: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE
description: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE は、デバイスサービスセッション用にデータを MB デバイスに書き込むようにミニポートドライバーに指示します。操作の完了ステータスを記述する NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 構造体を含む NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE ステータス通知。
ms.assetid: C1389D7D-3C8E-41B5-8E00-617D699699A2
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_SERVICE_SESSION_WRITE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 2c27711b22bab463e0262f795b82a6a431a3fec6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843855"
---
# <a name="oid_wwan_device_service_session_write"></a>OID\_WWAN\_デバイス\_サービス\_セッション\_書き込み


OID\_WWAN\_デバイス\_サービス\_セッション\_書き込みでは、デバイスサービスセッションのデータを MB デバイスに書き込むようにミニポートドライバーに指示します。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_サービス\_セッション\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete) 、 [**NDIS\_WWAN\_デバイス\_サービス\_セッション\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete)を含む完全な状態通知\_書き込み\_操作の完了ステータス。

デバイスサービスセッションが開いていない場合、ミニポートドライバーは NDIS\_STATUS\_アダプター\_\_を返す必要があります。

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


[**NDIS\_ステータス\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete)

[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write)

 

 




