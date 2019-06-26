---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ
description: ミニポート ドライバーでは、サービスのセッションで開いているデバイスにデータが受信されたことを MB サービスに通知するために NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 通知を使用します。NDIS_WWAN_DEVICE_SERVICE_SESSION_READ 構造体。
ms.assetid: 680C15DA-B37C-4A7C-B7BE-B13B3B050EC3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 037d00c44b3a6f0973c6182165ac1afcf619dfe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366612"
---
# <a name="ndisstatuswwandeviceservicesessionread"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション\_読み取り


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション\_MB サービス データが開いているデバイス サービスから受信されたことを通知するために読み取り通知セッションです。

ミニポート ドライバーでは、要請していないイベントを送信するのにこの通知のみ使用できます。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_セッション\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)構造体。

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


[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)

 

 




