---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION は、デバイスサービスセッションを開いたり閉じたりするようにミニポートドライバーに指示します。操作の結果を記述する NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 構造体を含む NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION ステータス通知。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_SERVICE_SESSION ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c14bb312773365fc1000a1edf5c6a2f404261277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843851"
---
# <a name="oid_wwan_device_service_session"></a>OID\_WWAN\_デバイス\_サービス\_セッション


OID\_WWAN\_デバイス\_サービス\_セッションは、デバイスサービスセッションを開いたり閉じたりするようにミニポートドライバーに指示します。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)NDIS\_WWAN\_設定されたサービス\_セッション状態通知。操作の結果を記述する[ **\_デバイス\_サービス\_セッション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)構造を設定します。

ミニポートドライバーは、指定されたデバイスのサービスまたは操作をサポートしていない場合に、サポートされていない\_ため、NDIS\_の状態\_返す必要があります。

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


[**NDIS\_WWAN\_\_デバイス\_サービス\_セッションの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)

[ **\_デバイス\_サービス\_セッションの NDIS\_ステータス\_。** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)

 

 




