---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_DEVICE_CAPS_EX クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知を使用します。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d3eda6be7161a70346333d55c24923f213edb9f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354825"
---
# <a name="ndisstatuswwandevicecapsex"></a>NDIS\_状態\_WWAN\_デバイス\_CAP\_例


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_デバイス\_CAP\_EX** MB サービスに以前の完了を通知するために通知[OID\_WWAN\_デバイス\_CAP\_EX](https://msdn.microsoft.com/library/windows/hardware/mt799830)クエリ要求。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_CAP\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782401)構造体。

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
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_CAP\_例](https://msdn.microsoft.com/library/windows/hardware/mt799830)

[**NDIS\_WWAN\_デバイス\_CAP\_例**](https://msdn.microsoft.com/library/windows/hardware/mt782401)

 

 




