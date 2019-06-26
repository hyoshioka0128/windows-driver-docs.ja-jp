---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES は、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状態通知がサポートされているデバイスの一覧にサービスの Guid を提供する NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体を格納しています。
ms.assetid: 12AB2235-DDF8-44CB-BD3D-61D0FFCB4080
ms.date: 08/08/2017
keywords: -OID_WWAN_ENUMERATE_DEVICE_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3033d3b57040e3ead19da911ded8dbda809b0ec4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375174"
---
# <a name="oidwwanenumeratedeviceservices"></a>OID\_WWAN\_ENUMERATE\_デバイス\_サービス


OID\_WWAN\_ENUMERATE\_デバイス\_サービスは、ミニポート ドライバーでサポートされるデバイスのサービスの一覧を返します。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)状態通知を含む、 [ **NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)サービスの Guid サポートされているデバイスの一覧を提供する構造体。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_サポートされている\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)

[**NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




