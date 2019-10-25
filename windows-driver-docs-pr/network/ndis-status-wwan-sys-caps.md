---
title: NDIS_STATUS_WWAN_SYS_CAPS_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SYS_CAPS_INFO 通知を使用して、以前の OID_WWAN_SYS_CAPS_INFO クエリ要求の完了を MB サービスに通知します。
ms.assetid: 653A35EC-29BB-458D-B33C-41EF6EF47A6E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SYS_CAPS_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 18a02c8404785648f903de3555bb239fc23f82e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844625"
---
# <a name="ndis_status_wwan_sys_caps_info"></a>NDIS\_ステータス\_WWAN\_SYS\_CAP\_情報


ミニポートドライバーは、 **NDIS の\_ステータス\_wwan\_sys\_cap\_情報**通知を使用して、MB サービスに対して、以前の[OID\_wwan\_sys\_cap\_info](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)の完了を通知します。クエリ要求。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_SYS\_CAPS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)構造体を使用します。

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
<td><p>Windows 10 バージョン1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_SYS\_CAP\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

 

 




