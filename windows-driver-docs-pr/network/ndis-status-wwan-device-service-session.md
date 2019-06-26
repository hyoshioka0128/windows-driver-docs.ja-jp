---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: ミニポート ドライバーでは、デバイス サービス セッション状態の OID_WWAN_DEVICE_SERVICE_SESSION によって発生した変更の完了を報告するのに、NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION を示す値を使用します。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 構造体。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9d72398ef20047bb1afd4ffafcb63445fb0d2f2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366608"
---
# <a name="ndisstatuswwandeviceservicesession"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_によってデバイス サービス セッション状態の変更の完了を報告するセッションを示す値を発信[OID\_WWAN\_デバイス\_サービス\_セッション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)構造体。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_サービス\_セッション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)

[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)

 

 




