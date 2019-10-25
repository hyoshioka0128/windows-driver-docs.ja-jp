---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 通知を使用して、OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS のクエリの完了を報告します。NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 構造体。
ms.assetid: 3EFEFB4B-6B13-44D7-8788-140B90103A93
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f4af6c66ea19541b61da16a89869f840eef98cc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843031"
---
# <a name="ndis_status_wwan_device_service_supported_commands"></a>NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド通知を使用して、OID\_WWAN のクエリの完了を報告し\_[デバイスを列挙\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)の構造を使用します。

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


[OID\_WWAN\_\_デバイス\_サービス\_コマンドを列挙する](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)

[**NDIS\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)

 

 




