---
title: KSPROPERTY\_チューナー\_モード\_キャップ
description: KSPROPERTY\_チューナー\_モード\_CAPS プロパティがチューニング モードの場合のアナログ テレビをサポートするチューナーまたは無線のチューニングの機能について説明します。 このプロパティを実装する必要があります。
ms.assetid: 521468df-40f5-4e52-9206-127e42ad5780
keywords:
- KSPROPERTY_TUNER_MODE_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85141bf98e0870dcd52f2dbaff5d167349878d3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355993"
---
# <a name="kspropertytunermodecaps"></a>KSPROPERTY\_チューナー\_モード\_キャップ


KSPROPERTY\_チューナー\_モード\_CAPS プロパティがチューニング モードの場合のアナログ テレビをサポートするチューナーまたは無線のチューニングの機能について説明します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_mode_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_CAPS_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)"><strong>KSPROPERTY_TUNER_MODE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、チューナーのチューニング機能を指定する ULONG です。

<a name="remarks"></a>注釈
-------

**StandardsSupported** 、KSPROPERTY のメンバー\_チューナー\_モード\_CAP\_S 構造体が現在のアナログ ビデオ標準を指定します。

ごとの別個のモードの (アナログ テレビ、デジタル テレビ、FM、AM、または DSS)、ミニドライバーは、最小値と最大の頻度などの機能を報告の決済調整の粒度、時間、および番号の入力。

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

[**KSPROPERTY\_チューナー\_モード\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)

 

 






