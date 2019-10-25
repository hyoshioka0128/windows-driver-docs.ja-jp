---
title: KSK プロパティ\_BDA\_RF\_チューナー\_範囲
description: クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_範囲を使用して、チューナーの範囲 (特定のキャリア周波数を検索するドメイン) を制御します。
ms.assetid: 2f2aa515-3f3c-419f-a817-0d597466ec85
keywords:
- KSPROPERTY_BDA_RF_TUNER_RANGE ストリーミングメディアデバイス
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
ms.openlocfilehash: 70aeaee6522dfa336b210bb856d088aec1c92837
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838074"
---
# <a name="ksproperty_bda_rf_tuner_range"></a>KSK プロパティ\_BDA\_RF\_チューナー\_範囲


クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_範囲を使用して、チューナーの範囲 (特定のキャリア周波数を検索するドメイン) を制御します。

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
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、チューナーノードの識別子を指定します。

プロパティ値は、設定するチューナーの範囲を指定します。

次を使用して、KSK プロパティ\_BDA\_RF\_チューナー\_範囲プロパティを指定します。

-   BDA\_範囲\_\_設定されていません (− 1) は、チューナーの範囲が設定されていないことを示します。

-   \_定義されていない BDA\_範囲\_(0) は、チューナーの範囲が定義されていないことを示します。

一部のチューナーは、特定のキャリア周波数を検索するドメインを定義するマルチスイッチなどの外部デバイスを制御します。 このプロパティは、チューナーの範囲を−1に設定します。これは、特定のチューニング領域にチューナーの範囲が使用されないこと、またはチューニング領域に固有の値に設定されることを意味します。

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
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






