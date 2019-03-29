---
title: KSPROPERTY\_MEDIASEEKING\_機能
description: KSPROPERTY\_MEDIASEEKING\_機能プロパティのフィルターのメディア シーク機能を取得します。
ms.assetid: f0ee8fed-cdb5-44f9-96c3-d6edf235ea35
keywords:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9fd9354408d7c60865addf848646a619c56ee59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580925"
---
# <a name="kspropertymediaseekingcapabilities"></a>KSPROPERTY\_MEDIASEEKING\_機能


KSPROPERTY\_MEDIASEEKING\_機能プロパティのフィルターのメディア シーク機能を取得します。

## <span id="ddk_ksproperty_mediaseeking_capabilities_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_CAPABILITIES_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KS_SEEKING_CAPABILITIES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

このプロパティを取得するフィルターの機能には、メディアの再生中に現在位置を取得または停止モード、または下位を再生する期間を取得する前後をシークする、絶対位置をシーク機能が含まれます。 これらが全体として、フィルターの機能であることに注意してください。このプロパティは、DirectShow フィルターしない暗証番号 (pin)、単位でのみこのような機能を照会する場所の機能をシークするマップに設計されています。

このプロパティがサポートされていない場合、フィルターに位置情報が必要ないことと、パススルーとフィルターを扱うことができますと見なされます。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






