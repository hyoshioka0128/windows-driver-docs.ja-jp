---
title: KSPROPERTY\_FMRX\_ENDPOINTID
description: KSTOPOLOGY\_ENDPOINTID プロパティには、FM ラジオ出力レンダー/エンドポイントのエンドポイント ID が含まれています。
ms.assetid: C71DA54C-069D-43F6-8107-AF109D4CA967
keywords:
- KSPROPERTY_FMRX_ENDPOINTID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_ENDPOINTID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a6f58bd1b95a0eba5ab2d600a8a7a8a56c83b49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332728"
---
# <a name="kspropertyfmrxendpointid"></a>KSPROPERTY\_FMRX\_ENDPOINTID


[ **KSTOPOLOGY\_ENDPOINTID** ](https://msdn.microsoft.com/library/windows/hardware/mt169886)プロパティには、FM ラジオ出力レンダー/エンドポイントのエンドポイント ID が含まれています。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169886" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169886)"><strong>KSTOPOLOGY_ENDPOINTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型[ **KSTOPOLOGY\_ENDPOINTID** ](https://msdn.microsoft.com/library/windows/hardware/mt169886)名前や FM ラジオに関連付けられているトポロジのエンドポイントの暗証番号 (pin) の ID を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_FMRX\_ENDPOINTID**プロパティ要求がレンダリング FM ラジオ用のエンドポイントの名前と現在の暗証番号 (pin) の ID を返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[KSPROPSETID\_FMRXTopology](kspropsetid-fmrxtopology.md)

 

 






