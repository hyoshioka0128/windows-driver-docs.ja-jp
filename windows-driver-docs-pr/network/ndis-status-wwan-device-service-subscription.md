---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知を使用して、OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS セット要求への応答でデバイスのサービス サブスクリプションに関する MB サービスに通知します。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 構造体。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a11ecfb82123353d3b1b890c6d7bde2560c933de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344230"
---
# <a name="ndisstatuswwandeviceservicesubscription"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_サブスクリプション


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_MB サービスへの応答内のサービス サブスクリプションにデバイスに通知するためにサブスクリプションの通知、 [OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://msdn.microsoft.com/library/windows/hardware/hh440096)セットの要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

このを示す値を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://msdn.microsoft.com/library/windows/hardware/hh439839)構造体。

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


[OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://msdn.microsoft.com/library/windows/hardware/hh440096)

[**NDIS\_WWAN\_デバイス\_サービス\_サブスクリプション**](https://msdn.microsoft.com/library/windows/hardware/hh439839)

 

 




