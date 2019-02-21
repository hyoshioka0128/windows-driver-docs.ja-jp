---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知を使用して、OID_WWAN_ENUMERATE_DEVICE_SERVICES クエリ要求の完了に関する MB サービスに通知します。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 構造体。
ms.assetid: 6364DDF7-CE68-4E00-8532-221DD209F145
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b30cecd45963cb3bef45082c087a5b1a004f56db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550638"
---
# <a name="ndisstatuswwansupporteddeviceservices"></a>NDIS\_状態\_WWAN\_サポートされている\_デバイス\_サービス


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_サポートされている\_デバイス\_サービス通知の完了に関する MB サービスに通知を[OID\_WWAN\_ENUMERATE\_デバイス\_サービス](https://msdn.microsoft.com/library/windows/hardware/hh846220)要求のクエリを実行します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://msdn.microsoft.com/library/windows/hardware/hh831867)構造体。

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


[OID\_WWAN\_ENUMERATE\_デバイス\_サービス](https://msdn.microsoft.com/library/windows/hardware/hh846220)

[**NDIS\_WWAN\_サポートされている\_デバイス\_サービス**](https://msdn.microsoft.com/library/windows/hardware/hh831867)

 

 




