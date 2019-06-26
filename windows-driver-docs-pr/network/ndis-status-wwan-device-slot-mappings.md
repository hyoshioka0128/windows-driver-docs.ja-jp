---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知を使用して、前の OID_WWAN_DEVICE_SLOT_MAPPING_INFO クエリの完了に関する MB サービスに通知するまたは要求を設定します。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9dc108d11370ee5886afc8388abad464c1865fdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366602"
---
# <a name="ndisstatuswwandeviceslotmappinginfo"></a>NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**MB サービスに通知する通知、前回の完了[OID\_WWAN\_デバイス\_スロット\_マッピング\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)クエリまたは要求を設定します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)構造体。

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


[OID\_WWAN\_デバイス\_スロット\_マッピング\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

 

 




