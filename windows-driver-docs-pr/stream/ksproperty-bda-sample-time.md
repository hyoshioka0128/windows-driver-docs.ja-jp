---
title: KSPROPERTY\_BDA\_サンプル\_時間
description: クライアントを使用して、KSPROPERTY\_BDA\_サンプル\_レベルと品質を平均する信号をサンプル時間を決定します。
ms.assetid: 53252e11-2a18-42d5-aed8-99052a2b0f21
keywords:
- KSPROPERTY_BDA_SAMPLE_TIME ストリーミング メディア デバイス
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
ms.openlocfilehash: 5a628ae779152d791dda2dc4a61ae75344527473
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361139"
---
# <a name="kspropertybdasampletime"></a>KSPROPERTY\_BDA\_サンプル\_時間


クライアントを使用して、KSPROPERTY\_BDA\_サンプル\_レベルと品質を平均する信号をサンプル時間を決定します。

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
<td><p>Pin またはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返される値は、ミリ秒単位でサンプルの時間を指定します。

たびにクライアントが要求シグナルの statistics プロパティ、ノードは、n KSPROPERTY により示される値は最後の n ミリ秒の平均値を報告する必要があります\_BDA\_サンプル\_時間。 時刻の値が設定されていない場合、またはドライバーが KSPROPERTY をサポートしていない場合\_BDA\_サンプル\_時間、ドライバーの既定 100 ミリ秒のサンプリング時間にする必要があります。

ドライバーは、最近完了したサンプル期間の時刻の値を報告できます。

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

[**KSPROPERTY\_BDA\_信号\_品質**](ksproperty-bda-signal-quality.md)

[**KSPROPERTY\_BDA\_信号\_強度**](ksproperty-bda-signal-strength.md)

 

 






