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
ms.openlocfilehash: 0618a49d946f58712bc732da801532a3924a1874
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373092"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)"><strong>KSPROPERTY_CROSSBAR_CAPS_S</strong></a></p></td>
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

[**KSPROPERTY\_クロスバー\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)

 

 






