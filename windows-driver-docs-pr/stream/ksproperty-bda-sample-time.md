---
title: KSK プロパティ\_BDA\_サンプル\_時間
description: クライアントは、KSK プロパティ\_BDA\_サンプル\_時間を使用して、シグナルレベルと品質の平均を示すサンプル時間を決定します。
ms.assetid: 53252e11-2a18-42d5-aed8-99052a2b0f21
keywords:
- KSPROPERTY_BDA_SAMPLE_TIME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SAMPLE_TIME
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b3b0ccf4f70ec576eb9962df92e8a01b7da2fe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838072"
---
# <a name="ksproperty_bda_sample_time"></a>KSK プロパティ\_BDA\_サンプル\_時間


クライアントは、KSK プロパティ\_BDA\_サンプル\_時間を使用して、シグナルレベルと品質の平均を示すサンプル時間を決定します。

## <span id="ddk_ksproperty_bda_sample_time_ks"></span><span id="DDK_KSPROPERTY_BDA_SAMPLE_TIME_KS"></span>


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
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

戻り値は、サンプル時間をミリ秒単位で指定します。

クライアントが "signal statistics" プロパティを要求するたびに、ノードは最後の n ミリ秒の平均値を報告する必要があります。 n は、KSK プロパティ\_BDA\_SAMPLE\_TIME によって示される値です。 時刻値が設定されていない場合、またはドライバーが KSK プロパティ\_BDA\_サンプル\_時刻をサポートしていない場合、ドライバーの既定の時間は100ミリ秒になります。

ドライバーは、最近完了したサンプル期間の時刻値を報告できます。

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

[**KSK プロパティ\_BDA\_シグナル\_品質**](ksproperty-bda-signal-quality.md)

[**KSK プロパティ\_BDA\_シグナル\_強度**](ksproperty-bda-signal-strength.md)

 

 






