---
title: KSPROPERTY\_FMRX\_ボリューム
description: KSPROPERTY\_FMRX\_ボリューム プロパティは、FM ラジオの量を制御します。
ms.assetid: 28650DEB-EA09-4E30-A1A7-179D1E1A641F
keywords:
- KSPROPERTY_FMRX_VOLUME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a06caefd922bccec83190aee6a87b6cff3c722ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332724"
---
# <a name="kspropertyfmrxvolume"></a>KSPROPERTY\_FMRX\_ボリューム


**KSPROPERTY\_FMRX\_ボリューム**プロパティは、FM ラジオの量を制御します。

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
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は LONG 型の FM ラジオのボリュームを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_FMRX\_ボリューム**プロパティ要求は、FM ラジオの体積を返します。

<a name="remarks"></a>注釈
-------

FM ボリュームとルーティング (エンドポイントの選択) によって制御されます、 **KSPROPERTY\_FMRX\_ボリューム**と[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)トポロジ フィルターのプロパティ。 基本的なサポート、 **KSPROPERTY\_FMRX\_ボリューム**プロパティは、最小のボリューム、最大のボリュームとボリュームの範囲を返す必要があります。

<a name="requirements"></a>必要条件
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
<td align="left"><p>サポートなし</p></td>
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

 

 





