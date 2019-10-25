---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知を使用して、OID_WWAN_ENUMERATE_DEVICE_SERVICES クエリ要求の完了を MB サービスに通知します。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体。
ms.assetid: 6364DDF7-CE68-4E00-8532-221DD209F145
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 7a14441f7334252fe64ab176e3eb4ea030b282d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844627"
---
# <a name="ndis_status_wwan_supported_device_services"></a>サポートされているデバイス\_サービス\_、NDIS\_ステータス\_WWAN\_


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_サポートされているデバイス\_サービス通知を使用し\_て、MB サービスに対して OID\_の完了を通知し\_[デバイス\_サービスを列挙\_ます。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)クエリ要求。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、[**サポートされている\_デバイス\_サービスの構造\_、NDIS\_WWAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)を使用します。

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


[OID\_WWAN\_\_デバイス\_サービスを列挙する](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)

[**デバイス\_サービス\_サポートされている NDIS\_WWAN\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




