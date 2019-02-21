---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: ミニポート ドライバーでは、デバイス サービス セッション状態の OID_WWAN_DEVICE_SERVICE_SESSION によって発生した変更の完了を報告するのに、NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION を示す値を使用します。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 構造体。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e7044703a24ef054ef9eb084a6f6ed7f2c79b9d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560230"
---
# <a name="ndisstatuswwandeviceservicesession"></a>NDIS\_状態\_WWAN\_デバイス\_サービス\_セッション


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_サービス\_によってデバイス サービス セッション状態の変更の完了を報告するセッションを示す値を発信[OID\_WWAN\_デバイス\_サービス\_セッション](https://msdn.microsoft.com/library/windows/hardware/hh846218)します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh831858)構造体。

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


[OID\_WWAN\_デバイス\_サービス\_セッション](https://msdn.microsoft.com/library/windows/hardware/hh846218)

[**NDIS\_WWAN\_デバイス\_サービス\_セッション\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh831858)

 

 




