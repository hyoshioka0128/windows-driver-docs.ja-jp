---
title: KSPROPERTY\_チューナー\_入力
description: KSPROPERTY\_チューナー\_入力プロパティは、チューナーとアンテナのケーブル チューナーの入力間での選択など、現在のチューニング モードでの入力をについて説明します。 このプロパティを実装する必要があります。
ms.assetid: b2c92531-ad1f-4152-a98d-7cae9c2c940c
keywords:
- KSPROPERTY_TUNER_INPUT ストリーミング メディア デバイス
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
ms.openlocfilehash: 713d64e09f052c5e8903e070693d93cb5fb6e118
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577852"
---
# <a name="kspropertytunerinput"></a>KSPROPERTY\_チューナー\_入力


KSPROPERTY\_チューナー\_入力プロパティは、チューナーとアンテナのケーブル チューナーの入力間での選択など、現在のチューニング モードでの入力をについて説明します。 このプロパティを実装する必要があります。

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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565856" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565856)"><strong>KSPROPERTY_TUNER_INPUT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、物理的なチューナーの入力の数値インデックスを指定する ULONG です。 この値は 0 (数の入力-1) までの範囲でなければなりません。

<a name="remarks"></a>コメント
-------

**InputIndex** 、KSPROPERTY のメンバー\_チューナー\_入力\_S 構造体が現在チューナー入力インデックスを指定します。

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

[**KSPROPERTY\_チューナー\_入力\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565856)

 

 






