---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 状態では、メディア固有の状態を示します。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_MEDIA_SPECIFIC_INDICATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 719eaa093b2dc54db386ed7894aeb609a5809812
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373926"
---
# <a name="ndisstatusmediaspecificindication"></a>NDIS\_状態\_メディア\_特定\_を示す値


NDIS\_状態\_メディア\_特定\_表示状態をメディア固有の状態を示します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、メディア固有の状態インジケーターを行う呼び出すことによって、 [ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)関数と、 **StatusCode**のメンバー、 [**NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication) NDIS に設定\_状態\_メディア\_特定\_を示す値。 **StatusBuffer**ドライバーに割り当てられたバッファーを指し、この構造体のメンバー。 バッファーにはで指定されている状態の表示に固有の形式でデータが含まれています、 **StatusCode**メンバー。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

 

 




