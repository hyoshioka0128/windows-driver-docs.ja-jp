---
title: KSEVENT\_制御\_変更
description: KSEVENT\_CONTROL\_CHANGE イベントは、ハードウェアボリューム制御ノブ、ミュートスイッチ、またはその他の種類の手動コントロールを表すノードで、制御値の変更が発生したことを示します。使用状況の概要 TableTargetEvent Descriptor TypeEvent 値 TypePinKSE\_NODEKSEVENTDATA イベント値の種類 (操作データ) は、イベントに使用する通知の種類を指定する KSEVENTDATA 構造です。
ms.assetid: 32d8e14c-f21d-4bac-8d98-8aca40e30b60
keywords:
- KSEVENT_CONTROL_CHANGE オーディオデバイス
topic_type:
- apiref
api_name:
- KSEVENT_CONTROL_CHANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02f04d90e0e615ab486232c44a51f676451c236
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833143"
---
# <a name="ksevent_control_change"></a>KSEVENT\_制御\_変更


KSEVENT\_CONTROL\_CHANGE イベントは、ハードウェアボリューム制御ノブ、ミュートスイッチ、またはその他の種類の手動コントロールを表すノードで、制御値の変更が発生したことを示します。

**使用状況の概要テーブル**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">対象</th>
<th align="left">イベント記述子の種類</th>
<th align="left">イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の種類 (操作データ) は、イベントに使用する通知の種類を指定する KSEVENTDATA 構造体です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSE\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**PCEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)

[**PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

 

 






