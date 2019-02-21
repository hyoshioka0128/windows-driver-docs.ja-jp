---
title: KSPROPERTY\_クロスバー\_キャップ
description: KSPROPERTY\_クロスバー\_CAPS プロパティは、デバイス (クロスバーの入力と出力ピンの数) のクロスバー機能を取得します。 このプロパティを実装する必要があります。
ms.assetid: f7dd806c-065d-48c7-ab58-3f5ef95451d5
keywords:
- KSPROPERTY_CROSSBAR_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78ddd12b15bb56efb6207bee26e218144027ab3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538988"
---
# <a name="kspropertycrossbarcaps"></a>KSPROPERTY\_クロスバー\_キャップ


KSPROPERTY\_クロスバー\_CAPS プロパティは、デバイス (クロスバーの入力と出力ピンの数) のクロスバー機能を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_crossbar_caps_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAPS_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565120" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565120)"><strong>KSPROPERTY_CROSSBAR_CAPS_S</strong></a></p></td>
<td><p>ULONGs のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、クロスバーのオーディオおよびビデオの入力ピンの数を指定する ULONGs のペアとクロスバーのオーディオおよびビデオ出力ピンの数です。

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

[**KSPROPERTY\_クロスバー\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565120)

 

 






