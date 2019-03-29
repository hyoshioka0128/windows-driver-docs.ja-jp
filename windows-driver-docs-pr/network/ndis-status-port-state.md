---
title: NDIS_STATUS_PORT_STATE
description: NDIS ポートをサポートするミニポート ドライバーでは、NDIS ポートの状態の変化を示す、NDIS_STATUS_PORT_STATE 状態を示す値を使用します。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PORT_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1b27ceec7371a06e5270b45071dcfa809274532c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580453"
---
# <a name="ndisstatusportstate"></a>NDIS\_状態\_ポート\_状態


NDIS ポートをサポートするミニポート ドライバーを使用して、NDIS\_状態\_ポート\_NDIS ポートの状態の変化を示す状態表示の状態。

<a name="remarks"></a>コメント
-------

ミニポート ドライバー ポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 **StatusBuffer**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)構造体。

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




