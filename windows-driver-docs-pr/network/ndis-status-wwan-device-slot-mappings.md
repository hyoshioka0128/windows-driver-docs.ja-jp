---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知を使用して、前の OID_WWAN_DEVICE_SLOT_MAPPING_INFO クエリの完了に関する MB サービスに通知するまたは要求を設定します。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 377091b9d384f111021c836f144c86816fffb241
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553834"
---
# <a name="ndisstatuswwandeviceslotmappinginfo"></a>NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報


ミニポート ドライバーを使用して、 **NDIS\_状態\_WWAN\_デバイス\_スロット\_マッピング\_情報**MB サービスに通知する通知、前回の完了[OID\_WWAN\_デバイス\_スロット\_マッピング\_情報](https://msdn.microsoft.com/library/windows/hardware/mt799831)クエリまたは要求を設定します。

ミニポート ドライバーは、この通知を使用して、不要なイベントを送信することはできません。

この通知を使用して、 [ **NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782403)構造体。

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
<td><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WWAN\_デバイス\_スロット\_マッピング\_情報](https://msdn.microsoft.com/library/windows/hardware/mt799831)

[**NDIS\_WWAN\_デバイス\_スロット\_マッピング\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt782403)

 

 




