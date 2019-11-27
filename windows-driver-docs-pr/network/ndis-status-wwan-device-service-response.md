---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE を示すメッセージを使用して、OID_WWAN_DEVICE_SERVICE_COMMAND のトランザクション完了応答を実装します。NDIS_WWAN_DEVICE_SERVICE_RESPONSE 構造体。
ms.assetid: 2817EAFA-7A9A-4DC1-B2B7-31E1F4E5E331
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
ms.localizationpriority: medium
ms.openlocfilehash: 9d04dfbb8de4abf3f31d69e1469e9602b3770e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842644"
---
# <a name="ndis_status_wwan_device_service_response"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_応答


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_応答の表示を使用して、 [OID\_WWAN\_デバイス\_サービス\_コマンドのトランザクション完了応答を実装します。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command).

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_応答**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)構造を使用します。

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


[OID\_WWAN\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)

[**NDIS\_WWAN\_デバイス\_サービス\_応答**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)

 

 




