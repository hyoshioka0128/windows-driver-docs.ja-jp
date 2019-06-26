---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 通知を使用して、OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS のクエリの完了を報告します。NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 構造体。
ms.assetid: 3EFEFB4B-6B13-44D7-8788-140B90103A93
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 13779876e95387e189ca1fab19f50a350fd1334f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384393"
---
# <a name="ndisstatuswwandeviceservicesupportedcommands"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド通知のクエリの完了を報告する[OID\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)構造体。

<a name="requirements"></a>必要条件
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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_ENUMERATE\_デバイス\_サービス\_コマンド](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)

[**NDIS\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)

 

 




