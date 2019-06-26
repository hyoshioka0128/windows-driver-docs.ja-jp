---
title: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE
description: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE は、デバイス サービス セッションの MB デバイスにデータを書き込むミニポート ドライバーに指示します。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 状態の通知操作の完了ステータスを記述する NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 構造体を格納しています。
ms.assetid: C1389D7D-3C8E-41B5-8E00-617D699699A2
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICE_SESSION_WRITE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d851f44db625c92c914235600638ac3b595f966a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358622"
---
# <a name="oidwwandeviceservicesessionwrite"></a>OID\_WWAN\_デバイス\_サービス\_セッション\_書き込み


OID\_WWAN\_デバイス\_サービス\_セッション\_書き込み MB デバイスにデバイスのサービス セッションのデータを書き込むミニポート ドライバーに指示します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete) を格納している状態の通知[ **NDIS\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete)構造体を操作の状態を完了します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_アダプター\_いない\_デバイス、サービスのセッションが開いていない場合は開きます。

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


[**NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション\_書き込み\_完了**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete)

[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write)

 

 




