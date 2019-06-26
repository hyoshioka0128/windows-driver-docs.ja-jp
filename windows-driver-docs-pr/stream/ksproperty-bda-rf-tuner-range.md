---
title: KSPROPERTY\_BDA\_RF\_チューナー\_範囲
description: クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_範囲は、チューナー範囲を制御する特定のキャリア周波数を検索するドメイン。
ms.assetid: 2f2aa515-3f3c-419f-a817-0d597466ec85
keywords:
- KSPROPERTY_BDA_RF_TUNER_RANGE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_RANGE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7abc9ce5aa97de256624367630b22a3d53281ed2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361135"
---
# <a name="kspropertybdarftunerrange"></a>KSPROPERTY\_BDA\_RF\_チューナー\_範囲


クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_範囲は、チューナー範囲を制御する特定のキャリア周波数を検索するドメイン。

## <span id="ddk_ksproperty_bda_rf_tuner_range_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_RANGE_KS"></span>


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

プロパティの値を設定するチューナーの範囲を指定します。

指定、KSPROPERTY\_BDA\_RF\_チューナー\_で範囲のプロパティ。

-   BDA\_範囲\_いない\_セット (-1) では、チューナーの範囲が設定されていないことを示します。

-   BDA\_範囲\_いない\_定義 (0) では、チューナーの範囲が定義されていないことを示します。

いくつかのチューナーを複数のスイッチ、特定のキャリア周波数を検索するドメインを定義するなどの外部のデバイスを制御します。 このプロパティは、− 1、チューナーの範囲が特定のチューニングの領域を使用していないことを意味するか、チューニングの領域に固有の値にチューナーの範囲を設定します。

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

 

 






