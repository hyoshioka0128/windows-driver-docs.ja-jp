---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES は、ミニポートドライバーでサポートされているデバイスサービスの一覧を返します。サポートされているデバイスサービス Guid の一覧を提供する NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体を含む NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS ステータス通知。
ms.assetid: 12AB2235-DDF8-44CB-BD3D-61D0FFCB4080
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_ENUMERATE_DEVICE_SERVICES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 47279d09418e78a2359b296a4e2f19ef7a599141
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843843"
---
# <a name="oid_wwan_enumerate_device_services"></a>OID\_WWAN\_\_デバイス\_サービスを列挙する


OID\_WWAN\_\_デバイス\_サービスを列挙すると、ミニポートドライバーでサポートされているデバイスサービスの一覧が返されます。

Set 要求はサポートされていません。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS\_の状態\_返して、元の要求に必要な\_を示し、後で[**ndis\_ステータス\_WWAN\_デバイスに送信する必要があり\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)サポートされているデバイスサービスの guid の一覧を提供する[**NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)構造を含む\_コマンド\_サポートされています。

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

[**デバイス\_サービス\_サポートされている NDIS\_WWAN\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




