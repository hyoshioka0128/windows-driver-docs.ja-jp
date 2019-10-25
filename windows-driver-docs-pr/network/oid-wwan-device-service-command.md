---
title: OID_WWAN_DEVICE_SERVICE_COMMAND
description: OID_WWAN_DEVICE_SERVICE_COMMAND を使用すると、ミニポートドライバーはベンダー固有のコマンドを実装できます。NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE がトランザクションを完了したときに応答を提供するベンダー定義構造 (NDIS_WWAN_DEVICE_SERVICE_COMMAND) を含むステータス通知。
ms.assetid: 296E2D23-6EDA-4480-91A3-B6CB39243DAD
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_DEVICE_SERVICE_COMMAND ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a046905f185a5d8a0b736997b15fbe9fb1f21493
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843857"
---
# <a name="oid_wwan_device_service_command"></a>OID\_WWAN\_デバイス\_サービス\_コマンド


OID\_WWAN\_デバイス\_サービス\_コマンドを使用すると、ミニポートドライバーでベンダー固有のコマンドを実装できます。

クエリとセットの両方の要求がサポートされています。

ミニポートドライバーは、クエリと要求を非同期に処理し、最初に NDIS\_\_状態を返し、元の要求に必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_SERVICE\_応答**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)状態通知。トランザクションの完了時に応答を提供するために、ベンダー定義構造 ([**NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)) を含んでいます。

ミニポートドライバーは、指定されたデバイスのサービスまたは操作をサポートしていない場合に、サポートされていない\_ため、NDIS\_の状態\_返される必要があります。

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


[**NDIS\_ステータス\_WWAN\_デバイス\_サービス\_応答**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)

[**NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)

 

 




