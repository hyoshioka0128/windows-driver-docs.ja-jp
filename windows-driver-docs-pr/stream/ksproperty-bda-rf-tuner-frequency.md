---
title: KSPROPERTY\_BDA\_RF\_チューナー\_頻度
description: クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_KSPROPERTY と共に頻度\_BDA\_RF\_チューナー\_頻度\_乗数チューナーのノードの頻度の設定を制御します。
ms.assetid: 0bcecf33-06d5-4b07-8602-da97db5c1306
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad98d3a8ad0d35ff82e63001b260fc4dd372b061
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368850"
---
# <a name="kspropertybdarftunerfrequency"></a>KSPROPERTY\_BDA\_RF\_チューナー\_頻度


クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_KSPROPERTY と共に頻度\_BDA\_RF\_チューナー\_頻度\_乗数チューナーのノードの頻度の設定を制御します。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_KS"></span>


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

プロパティの値を設定する基本の頻度を指定します。

KSPROPERTY を指定する\_BDA\_RF\_チューナー\_使用頻度のプロパティ。

-   BDA\_頻度\_いない\_セット (-1) では、頻度が設定されていないことを示します。

-   BDA\_頻度\_いない\_定義 (0) では、頻度が定義されていないことを示します。

場合、KSPROPERTY\_BDA\_RF\_チューナー\_頻度\_乗数プロパティ BDA の乗数を指定する\_頻度\_乗数\_いない\_セット (− 1) または BDA\_頻度\_乗数\_いない\_(0) を定義し、KSPROPERTY\_BDA\_RF\_チューナー\_頻度プロパティキロ ヘルツ (kHz) で、頻度を指定します。 また、ミニドライバーがハンドラーを設定 ([*KStrSetPropertyHandler*](https://docs.microsoft.com/previous-versions/ff567200(v=vs.85))) 頻度の乗数のプロパティが呼び出されないため、ミニドライバーが指定された頻度が表されることを決定する必要がありますkHz (1 Hz x 1000) の単位。 実際には、既定の乗数値は 1000 です。 詳細については、次を参照してください。 [BDA チューナーのノードの周波数のプロパティにアクセスする](https://docs.microsoft.com/windows-hardware/drivers/stream/accessing-frequency-properties-of-a-bda-tuner-node)します。

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

[**KSPROPERTY\_BDA\_RF\_チューナー\_頻度\_乗数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)

 

 






