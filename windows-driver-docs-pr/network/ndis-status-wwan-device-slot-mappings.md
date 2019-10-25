---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: ミニポートドライバーは、NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知を使用して、以前の OID_WWAN_DEVICE_SLOT_MAPPING_INFO クエリまたは set 要求の完了を MB サービスに通知します。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 56a7f02898b1773d20cce535f5232044142befc6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843029"
---
# <a name="ndis_status_wwan_device_slot_mapping_info"></a>NDIS\_ステータス\_WWAN\_デバイス\_スロット\_\_情報のマッピング


ミニポートドライバーは、 **NDIS\_ステータス\_wwan\_デバイス\_スロット\_\_情報**通知のマッピングを使用して、MB サービスに対して、以前の[OID\_WWAN\_デバイスの完了を通知し\_スロット\_\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)クエリまたは設定要求をマップしています。

ミニポートドライバーは、この通知を使用して一方的なイベントを送信することはできません。

この通知では、 [**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)構造を使用します。

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


[OID\_WWAN\_デバイス\_スロット\_マッピング\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

 

 




