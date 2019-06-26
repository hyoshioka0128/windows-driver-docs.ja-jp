---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION では、ミニポート ドライバーを開くか、デバイス サービス セッションを閉じるよう指示します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状態の通知操作の結果を記述する NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 構造体を格納しています。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICE_SESSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a6f7880d4ad623390fb39fa4194488b17155d72f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358605"
---
# <a name="oidwwandeviceservicesession"></a>OID\_WWAN\_デバイス\_サービス\_セッション


OID\_WWAN\_デバイス\_サービス\_セッションを開くか、デバイス サービス セッションを閉じるミニポート ドライバーに指示します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)状態通知を含む、 [ **NDIS\_WWAN\_設定\_デバイス\_サービス\_セッション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)操作の結果を記述する構造体。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_指定したデバイスのサービスまたは操作をサポートしていない場合にサポートされます。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_デバイス\_サービス\_セッション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)

[**NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)

 

 




