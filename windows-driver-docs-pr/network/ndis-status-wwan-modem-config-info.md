---
title: NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_MODEM_CONFIG_INFO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_MODEM_CONFIG_INFO 通知を使用します。
ms.assetid: 9D56BCE1-2CCF-4BD0-A646-4510642EB08A
keywords:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO、ネットワーク ドライバーが Windows Vista 以降
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
api_location:
- ndis.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9763e582e0470c8f40eb09d7d4401052cf351158
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535351"
---
# <a name="ndisstatuswwanmodemconfiginfo"></a>NDIS_STATUS_WWAN_MODEM_CONFIG_INFO


MBB ドライバーを使用して、 **NDIS_STATUS_WWAN_MODEM_CONFIG_INFO** MB サービスに前回の完了を通知するために通知[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)クエリ要求。

MBB ドライバーが、要請していないに送信する必要がありますのみ**NDIS_STATUS_WWAN_MODEM_CONFIG_INFO**モデムの構成の状態が変更されたとき。

この通知を使用して、 [ **NDIS_WWAN_MODEM_CONFIG_INFO** ](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)構造体。

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
<td><p>Windows 10 バージョン 1709</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)

[**NDIS_WWAN_MODEM_CONFIG_INFO**](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)
 

