---
title: KSEVENT\_コントロール\_変更
description: KSEVENT\_コントロール\_変更イベントは、ハードウェア ボリューム コントロールのノブ、ミュート スイッチ、または手動のコントロールの他の種類を表すノードにあるコントロールの値の変更が発生したことを示します。使用状況概要 TableTargetEvent 記述子 TypeEvent 値 TypePinKSE\_NODEKSEVENTDATA イベント値の型 (データの操作) は、イベントで使用する通知の種類を指定する KSEVENTDATA 構造体。
ms.assetid: 32d8e14c-f21d-4bac-8d98-8aca40e30b60
keywords:
- KSEVENT_CONTROL_CHANGE オーディオ デバイス
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
ms.openlocfilehash: 076d3e98ef978315ea4ef1955c2b7a90f0f8e1ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333352"
---
# <a name="kseventcontrolchange"></a>KSEVENT\_コントロール\_変更


KSEVENT\_コントロール\_変更イベントは、ハードウェア ボリューム コントロールのノブ、ミュート スイッチ、または手動のコントロールの他の種類を表すノードにあるコントロールの値の変更が発生したことを示します。

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
<th align="left">イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の型 (データの操作) は、イベントを使用する通知の種類を指定する KSEVENTDATA 構造です。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**サウンド\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff561937)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**PCEVENT\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff537692)

[**PCEVENT\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537693)

[IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)

 

 






