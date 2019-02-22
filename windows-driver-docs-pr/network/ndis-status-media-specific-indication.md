---
title: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION
description: NDIS_STATUS_MEDIA_SPECIFIC_INDICATION 状態では、メディア固有の状態を示します。
ms.assetid: 983ffff1-5157-46ae-b4ce-31ee1aa55955
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_MEDIA_SPECIFIC_INDICATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 865d64e7277b6a34f038df2291c043b4fabcef94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556805"
---
# <a name="ndisstatusmediaspecificindication"></a>NDIS\_状態\_メディア\_特定\_を示す値


NDIS\_状態\_メディア\_特定\_表示状態をメディア固有の状態を示します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、メディア固有の状態インジケーターを行う呼び出すことによって、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)関数と、 **StatusCode**のメンバー、 [**NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373) NDIS に設定\_状態\_メディア\_特定\_を示す値。 **StatusBuffer**ドライバーに割り当てられたバッファーを指し、この構造体のメンバー。 バッファーにはで指定されている状態の表示に固有の形式でデータが含まれています、 **StatusCode**メンバー。

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


[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




