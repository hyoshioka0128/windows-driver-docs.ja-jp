---
title: NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_MODEM_CONFIG_INFO 通知を使用して、以前の OID_WWAN_MODEM_CONFIG_INFO クエリ要求の完了を MB サービスに通知します。
ms.assetid: 9D56BCE1-2CCF-4BD0-A646-4510642EB08A
keywords:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO、Windows Vista 以降のネットワークドライバー
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
ms.openlocfilehash: 1f896547ed26840022f9a2680f5ff4db8c05c059
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843277"
---
# <a name="ndis_status_wwan_modem_config_info"></a>NDIS_STATUS_WWAN_MODEM_CONFIG_INFO


MBB ドライバーは、 **NDIS_STATUS_WWAN_MODEM_CONFIG_INFO**通知を使用して、以前の[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)クエリ要求の完了を MB サービスに通知します。

MBB ドライバーは、モデムの構成状態が変更された場合にのみ、一方的な**NDIS_STATUS_WWAN_MODEM_CONFIG_INFO**を送信する必要があります。

この通知では、 [**NDIS_WWAN_MODEM_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)構造体が使用されます。

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
<td><p>Windows 10 バージョン1709</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)

[**NDIS_WWAN_MODEM_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)
 

