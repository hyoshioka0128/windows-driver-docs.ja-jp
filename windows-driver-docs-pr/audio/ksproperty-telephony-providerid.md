---
title: KSPROPERTY\_テレフォニー\_PROVIDERID
description: KSPROPERTY\_テレフォニー\_PROVIDERID プロパティは、wave フィルター プロバイダーの識別子を関連付けるオーディオ ドライバーによって使用されます。
ms.assetid: A2BE85E3-068B-41C1-9791-69A929ECEC5C
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_PROVIDERID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 478f74769dbe29e39859badc697740c53fdd0840
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332574"
---
# <a name="kspropertytelephonyproviderid"></a>KSPROPERTY\_テレフォニー\_PROVIDERID


**KSPROPERTY\_テレフォニー\_PROVIDERID**プロパティは、wave フィルター プロバイダーの識別子を関連付けるオーディオ ドライバーによって使用されます。

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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>UINT</p></td>
</tr>
</tbody>
</table>

 

プロパティの値の型 UINT とプロバイダーの ID を指定します

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_PROVIDERID**プロパティ要求は、wave フィルターへのオーディオ ドライバーに関連付けているプロバイダーの ID を表す UINT 値を返します。

<a name="remarks"></a>注釈
-------

ラジオ スタックがプロバイダーの ID (実行プログラム ID) と呼び出しの種類の概念 (パケット回線交換または)、電話の呼び出しのインスタンスを特定のハードウェアのパスに接続します。 この概念は引き続き、オーディオ ドライバーにどのパスを使用するハードウェアでの通信に使用します。

このハードウェアのパスは、wave フィルターの各プロバイダーのプロパティを送信することによって制御されます。 オーディオ ドライバーでは、wave フィルター プロバイダーの ID を関連付けます。 このプロバイダーの ID は、関連付けられている携帯電話がストリーミング エンドポイントにも設定されます。 実行時に、wave フィルター プロバイダーの ID は変更はできません。 使用して、ドライバーからプロバイダーの ID をクエリは、オーディオ スタック、 **KSPROPERTY\_テレフォニー\_PROVIDERID**プロパティ。 このプロバイダーの ID が検出されると、そのプロバイダー ID のすべての呼び出しは、特定のウェーブ フィルターに送信されます。

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

 

 





