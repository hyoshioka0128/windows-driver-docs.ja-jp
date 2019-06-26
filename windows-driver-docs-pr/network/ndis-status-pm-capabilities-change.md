---
title: NDIS_STATUS_PM_CAPABILITIES_CHANGE
description: NDIS_STATUS_PM_CAPABILITIES_CHANGE 状態では、上にあるドライバーへのネットワーク アダプターの電源管理機能の変更を示します。
ms.assetid: 28a2ed15-606a-4a40-b975-b766815a02cc
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_CAPABILITIES_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 32757fb530afbef0e591a7d43a5a6d64294ca83c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368536"
---
# <a name="ndisstatuspmcapabilitieschange"></a>NDIS\_状態\_PM\_機能\_変更


NDIS\_状態\_PM\_機能\_状態の変更がドライバーに関連するネットワーク アダプターの電源管理機能の変更を示します。

<a name="remarks"></a>注釈
-------

NDIS 生成、NDIS\_状態\_PM\_機能\_変更状態の表示時に以前に報告された電源管理機能への更新が必要です。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)更新された電源管理機能を含む構造体。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 




