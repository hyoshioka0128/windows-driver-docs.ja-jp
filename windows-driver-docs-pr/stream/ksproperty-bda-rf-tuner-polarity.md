---
title: KSPROPERTY\_BDA\_RF\_チューナー\_極性
description: クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_極性チューナーのノードの極性設定を制御します。
ms.assetid: 6778b4ac-2444-4e27-ab80-5802dda09fdd
keywords:
- KSPROPERTY_BDA_RF_TUNER_POLARITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_POLARITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: edc0960b74e48a1d4428250ed87754950a8a1d37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580198"
---
# <a name="kspropertybdarftunerpolarity"></a>KSPROPERTY\_BDA\_RF\_チューナー\_極性


クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_極性チューナーのノードの極性設定を制御します。

## <span id="ddk_ksproperty_bda_rf_tuner_polarity_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_POLARITY_KS"></span>


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
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**NodeId** KSP のメンバー\_ノードは、チューナーのノードの識別子を指定します。

プロパティの値には、送信信号を設定する極性を指定します。

いくつかの転送では、特に衛星による伝送の信号を極性可能性があります。 このプロパティは、送信信号の極性に関するチューナー ノードを通知します。 極性列挙型には、信号の極性を指定する値が含まれています。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

[**極性**](https://msdn.microsoft.com/library/windows/hardware/ff567780)

 

 






