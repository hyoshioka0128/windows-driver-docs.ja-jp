---
title: NDIS_STATUS_PM_CAPABILITIES_CHANGE
description: NDIS_STATUS_PM_CAPABILITIES_CHANGE 状態では、上にあるドライバーへのネットワーク アダプターの電源管理機能の変更を示します。
ms.assetid: 28a2ed15-606a-4a40-b975-b766815a02cc
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_CAPABILITIES_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3fd5f1e2dadeb9ff4a8b2c9fbfb62fc7fc18f6d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552748"
---
# <a name="ndisstatuspmcapabilitieschange"></a>NDIS\_状態\_PM\_機能\_変更


NDIS\_状態\_PM\_機能\_状態の変更がドライバーに関連するネットワーク アダプターの電源管理機能の変更を示します。

<a name="remarks"></a>注釈
-------

NDIS 生成、NDIS\_状態\_PM\_機能\_変更状態の表示時に以前に報告された電源管理機能への更新が必要です。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)更新された電源管理機能を含む構造体。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




