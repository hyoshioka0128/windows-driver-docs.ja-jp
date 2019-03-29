---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_SLOT_INFO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_SLOT_INFO 通知を使用します。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SLOT_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bf37f07ecffec4fc3a53fe0a68e6e35de5678649
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578443"
---
# <a name="ndisstatuswwanslotinfo"></a>NDIS\_STATUS\_WWAN\_SLOT\_INFO


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_スロット\_情報**MB サービスに前回の完了を通知するために通知[OID\_WWAN\_スロット\_情報](https://msdn.microsoft.com/library/windows/hardware/mt799832)クエリ要求。

ミニポート ドライバーに送信できる、 **NDIS\_状態\_WWAN\_スロット\_情報**スロット/カードの状態が変更されたときに、要請していないイベントとして通知します。

この通知を使用して、 [ **NDIS\_WWAN\_スロット\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782408)構造体。

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


[OID\_WWAN\_SLOT\_INFO](https://msdn.microsoft.com/library/windows/hardware/mt799832)

[**NDIS\_WWAN\_SLOT\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt782408)

 

 




