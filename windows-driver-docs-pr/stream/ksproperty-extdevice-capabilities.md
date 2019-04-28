---
title: KSPROPERTY\_EXTDEVICE\_機能
description: KSPROPERTY\_EXTDEVICE\_機能プロパティは、外部のデバイスの機能を取得します。
ms.assetid: c408b4cf-2fd9-41b2-b182-47baa551fd93
keywords:
- KSPROPERTY_EXTDEVICE_CAPABILITIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aaab7b3b6d7523c972a45ba142bf0ce95bc4208
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364906"
---
# <a name="kspropertyextdevicecapabilities"></a>KSPROPERTY\_EXTDEVICE\_機能


KSPROPERTY\_EXTDEVICE\_機能プロパティは、外部のデバイスの機能を取得します。

## <span id="ddk_ksproperty_extdevice_capabilities_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_CAPABILITIES_KS"></span>


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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558699" data-raw-source="[&lt;strong&gt;DEVCAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558699)"><strong>DEVCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のデバイスの機能を表す DEVCAPS 構造です。

<a name="remarks"></a>注釈
-------

**機能**、KSPROPERTY のメンバー\_EXTDEVICE\_の構造を外部デバイスの機能を指定します。

<a name="requirements"></a>要件
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

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

[**DEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff558699)

 

 






