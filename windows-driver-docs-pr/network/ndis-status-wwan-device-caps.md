---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: ミニポート ドライバーでは、OID_WWAN_DEVICE_CAPS クエリ要求に応答する NDIS_STATUS_WWAN_DEVICE_CAPS 通知を使用します。 ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。この通知は、NDIS_WWAN_DEVICE_CAPS 構造体を使用します。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7db36d959fb538fcbb35a5c49f11b7519e47fb2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369882"
---
# <a name="ndisstatuswwandevicecaps"></a>NDIS\_状態\_WWAN\_デバイス\_キャップ


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_デバイス\_CAP 通知に応答する[OID\_WWAN\_デバイス\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569824)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)構造体。

<a name="remarks"></a>注釈
-------

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_キャップ](https://msdn.microsoft.com/library/windows/hardware/ff569824)

[**NDIS\_WWAN\_デバイス\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff567907)

 

 




