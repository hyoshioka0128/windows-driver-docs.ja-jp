---
title: KSK プロパティ\_チューナー\_STANDARD
description: KSK プロパティ\_チューナー\_標準プロパティは、現在のアナログビデオ標準を取得します。 このプロパティを実装する必要があります。
ms.assetid: b20dd01c-bd6b-4908-a3c4-eb2914eb54d0
keywords:
- KSPROPERTY_TUNER_STANDARD ストリーミングメディアデバイス
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
ms.openlocfilehash: 78f1b26e286856f17d68145e0920b2eb371b8d86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837899"
---
# <a name="ksproperty_tuner_standard"></a>KSK プロパティ\_チューナー\_STANDARD


KSK プロパティ\_チューナー\_標準プロパティは、現在のアナログビデオ標準を取得します。 このプロパティを実装する必要があります。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)"><strong>KSPROPERTY_TUNER_STANDARD_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、チューナーのチューニング標準を指定する ULONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_チューナー\_標準\_S 構造体の**標準**メンバーは、現在のアナログビデオ標準を指定します。

このプロパティは、現在のモードが KSK プロパティ\_チューナー\_モード\_TV になっている場合にのみ使用されます。

アナログテレビ信号は、NTSC、PAL、SECAM など、さまざまなアナログテレビ標準に従って放送できます。 クライアントは、KSK プロパティ\_チューナー\_MODE\_CAPS プロパティを使用して、サポートされている標準を照会します。また、KSK プロパティ\_チューナー\_STANDARD を使用して、TV チューナーデバイスの現在の標準を取得または設定します。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_チューナー\_STANDARD\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)

[**KSK プロパティ\_チューナー\_モード**](ksproperty-tuner-mode.md)

 

 






