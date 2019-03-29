---
title: KSPROPERTY\_EXTXPORT\_状態
description: KSPROPERTY\_EXTXPORT\_状態プロパティを設定または外部のデバイスのトランスポート モードと状態を取得します。
ms.assetid: c508b6ce-2a37-4fca-9edf-66700d9cbd15
keywords:
- KSPROPERTY_EXTXPORT_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb24fad8155abc27d2a270f794be19d1ba9a2fc7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580089"
---
# <a name="kspropertyextxportstate"></a>KSPROPERTY\_EXTXPORT\_状態


KSPROPERTY\_EXTXPORT\_状態プロパティを設定または外部のデバイスのトランスポート モードと状態を取得します。

## <span id="ddk_ksproperty_extxport_state_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565167" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565167)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568546" data-raw-source="[&lt;strong&gt;TRANSPORT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568546)"><strong>TRANSPORT_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、トランスポート\_現在のモードと外部のトランスポートの状態を記述する状態の構造体。 たとえば、モード設定されている場合 (一時停止) を固定するを再生する状態を設定する場合があります。

<a name="remarks"></a>コメント
-------

**XPrtState** 、KSPROPERTY のメンバー\_EXTXPORT\_の構造は、モードと状態を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)

[**トランスポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff568546)

 

 






