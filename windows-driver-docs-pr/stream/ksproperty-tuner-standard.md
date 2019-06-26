---
title: KSPROPERTY\_チューナー\_標準
description: KSPROPERTY\_チューナー\_標準プロパティは、現在のアナログ ビデオ標準を取得します。 このプロパティを実装する必要があります。
ms.assetid: b20dd01c-bd6b-4908-a3c4-eb2914eb54d0
keywords:
- KSPROPERTY_TUNER_STANDARD ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STANDARD
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71909d5b4bc7cb98543adc53329e145539bbc174
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355963"
---
# <a name="kspropertytunerstandard"></a>KSPROPERTY\_チューナー\_標準


KSPROPERTY\_チューナー\_標準プロパティは、現在のアナログ ビデオ標準を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_standard_ks"></span><span id="DDK_KSPROPERTY_TUNER_STANDARD_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)"><strong>KSPROPERTY_TUNER_STANDARD_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、チューナーのチューニングの標準を指定する ULONG です。

<a name="remarks"></a>注釈
-------

**標準**、KSPROPERTY のメンバー\_チューナー\_標準\_S 構造体が現在のアナログ ビデオ標準を指定します。

このプロパティは、現在のモードが KSPROPERTY 場合にのみ使用\_チューナー\_モード\_テレビです。

いくつか異なるアナログ テレビ標準に従って NTSC、PAL、SECAM などは、アナログ テレビ信号をブロードキャストすることができます。 クライアントの使用、KSPROPERTY\_チューナー\_モード\_CAPS プロパティに、サポートされている、標準のクエリを実行して、KSPROPERTY\_チューナー\_標準テレビ チューナー デバイスの現在の標準の設定を取得または。

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

[**KSPROPERTY\_チューナー\_標準\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)

[**KSPROPERTY\_チューナー\_モード**](ksproperty-tuner-mode.md)

 

 






