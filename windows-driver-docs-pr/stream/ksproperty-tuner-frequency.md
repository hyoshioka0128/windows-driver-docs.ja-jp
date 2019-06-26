---
title: KSPROPERTY\_チューナー\_頻度
description: KSPROPERTY\_チューナー\_頻度プロパティを設定または現在の頻度またはチューナーのチャネルを取得します。 このプロパティを実装する必要があります。
ms.assetid: ba6caf67-63c1-4a31-b93f-3b06b61244bf
keywords:
- KSPROPERTY_TUNER_FREQUENCY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_FREQUENCY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ca71ae173bf289ccde3388e6d1449a1550f87dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383975"
---
# <a name="kspropertytunerfrequency"></a>KSPROPERTY\_チューナー\_頻度


KSPROPERTY\_チューナー\_頻度プロパティを設定または現在の頻度またはチューナーのチャネルを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_TUNER_FREQUENCY_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)"><strong>KSPROPERTY_TUNER_FREQUENCY_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、チューナーの現在の頻度を指定する ULONG です。 この値は、ヘルツ (Hz) で指定されます。

<a name="remarks"></a>注釈
-------

**頻度**、KSPROPERTY のメンバー\_チューナー\_頻度\_の構造は、現在のチューナー頻度を指定します。

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

[**KSPROPERTY\_チューナー\_頻度\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)

 

 






