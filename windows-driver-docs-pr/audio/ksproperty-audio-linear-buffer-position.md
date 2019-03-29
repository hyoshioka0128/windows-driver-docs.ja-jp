---
title: KSPROPERTY\_オーディオ\_線形\_バッファー\_位置
description: KSPROPERTY\_オーディオ\_線形\_バッファー\_位置プロパティ要求を DMA をオーディオ バッファーからストリームの先頭からフェッチしたバイト数を表す数値を取得します。
ms.assetid: 08CC3164-2B8F-4368-8A34-6F8954992D3A
keywords:
- KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964f30dc61310665aee9875ffda0cd4066425477
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581931"
---
# <a name="kspropertyaudiolinearbufferposition"></a>KSPROPERTY\_オーディオ\_線形\_バッファー\_位置


KSPROPERTY\_オーディオ\_線形\_バッファー\_位置プロパティ要求を DMA をオーディオ バッファーからストリームの先頭からフェッチしたバイト数を表す数値を取得します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONGULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_線形\_バッファー\_位置プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





