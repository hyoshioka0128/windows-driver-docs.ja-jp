---
title: KSPROPERTY\_BDA\_RF\_チューナー\_トランスポンダー
description: クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_トランスポンダー トランスポンダーの適切な数のチューナーのノードに通知します。
ms.assetid: 00445260-a317-4341-baab-d1391f6748e4
keywords:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16b2e3c5f9cb763b0c4110f7e962ead0c328b9bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361142"
---
# <a name="kspropertybdarftunertransponder"></a>KSPROPERTY\_BDA\_RF\_チューナー\_トランスポンダー


クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_トランスポンダー トランスポンダーの適切な数のチューナーのノードに通知します。

## <span id="ddk_ksproperty_bda_rf_tuner_transponder_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_TRANSPONDER_KS"></span>


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
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**NodeId** KSP のメンバー\_ノードは、チューナーのノードの識別子を指定します。

プロパティの値は、トランスポンダー番号の設定を指定します。

一部のチューニングのスペースがあるすべてのハードウェアに組み込む頻度を取得する方法に関する情報。 これらのスペースのチューニングは、トランスポンダー数を指定します。 このプロパティは、このトランスポンダー数値のチューナーのノードを通知します。 チューナー ハードウェアは、中間の頻度を取得するために必要なチューニングの特性を自動的に判断し、ことができます。 この場合、その他のプロパティで、KSPROPSETID\_BdaFrequencyFilter プロパティ セットが − 1 に設定されます。

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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






