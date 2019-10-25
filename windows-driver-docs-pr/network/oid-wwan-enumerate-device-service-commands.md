---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS
description: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS は、デバイスサービスでサポートされているコマンドの一覧を返します。操作の結果を記述する NDIS_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 構造体を含む NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS ステータス通知。
ms.assetid: 9888E4EC-D4BB-4BAC-B20B-DFA51005EEDA
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a0122e4de6641c99a265d6c3e82d2a5980e0b76e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843846"
---
# <a name="oid_wwan_enumerate_device_service_commands"></a>OID\_WWAN\_\_デバイス\_サービス\_コマンドを列挙する


OID\_WWAN\_\_デバイスの列挙\_サービス\_コマンドを使用すると、デバイスサービスでサポートされているコマンドの一覧が返されます。

Set 要求はサポートされていません。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_の状態\_返して、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)の状態通知[**NDIS\_\_WWAN を含む\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)の結果を説明するコマンドの構造を列挙します。

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


[**NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)

[**NDIS\_WWAN\_\_デバイス\_サービス\_コマンドの列挙**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)

 

 




