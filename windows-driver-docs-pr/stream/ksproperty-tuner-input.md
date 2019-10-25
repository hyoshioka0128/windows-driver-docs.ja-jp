---
title: KSK プロパティ\_チューナー\_入力
description: KSK プロパティ\_チューナー\_入力プロパティは、ケーブルやアンテナチューナーの入力を選択するなど、現在のチューニングモードでのチューナーの入力を記述します。 このプロパティを実装する必要があります。
ms.assetid: b2c92531-ad1f-4152-a98d-7cae9c2c940c
keywords:
- KSPROPERTY_TUNER_INPUT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_INPUT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392e327406b8b2022468e94e1881082792128b6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837910"
---
# <a name="ksproperty_tuner_input"></a>KSK プロパティ\_チューナー\_入力


KSK プロパティ\_チューナー\_入力プロパティは、ケーブルやアンテナチューナーの入力を選択するなど、現在のチューニングモードでのチューナーの入力を記述します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_input_ks"></span><span id="DDK_KSPROPERTY_TUNER_INPUT_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)"><strong>KSPROPERTY_TUNER_INPUT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、物理的なチューナー入力の数値インデックスを指定する ULONG です。 この値は、0から (入力数-1) の範囲内である必要があります。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_チューナー\_入力\_S 構造体の**Inputindex**メンバーは、現在のチューナー入力インデックスを指定します。

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

[**KSK プロパティ\_チューナー\_入力\_S)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)

 

 






