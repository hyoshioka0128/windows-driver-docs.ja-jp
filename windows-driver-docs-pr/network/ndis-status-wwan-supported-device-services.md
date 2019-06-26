---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知を使用して、OID_WWAN_ENUMERATE_DEVICE_SERVICES クエリ要求の完了に関する MB サービスに通知します。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体。
ms.assetid: 6364DDF7-CE68-4E00-8532-221DD209F145
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6ea6919f395f5e3ee8b3ec88fac237e7d27cedce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372524"
---
# <a name="ndisstatuswwansupporteddeviceservices"></a>NDIS\_状態\_WWAN\_サポートされている\_デバイス\_サービス


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_サポートされている\_デバイス\_サービス通知の完了に関する MB サービスに通知を[OID\_WWAN\_ENUMERATE\_デバイス\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)要求のクエリを実行します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)構造体。

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


[OID\_WWAN\_ENUMERATE\_デバイス\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)

[**NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




