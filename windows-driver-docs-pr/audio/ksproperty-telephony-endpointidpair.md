---
title: KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR
description: KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR プロパティに携帯電話の音声ルーティングのレンダリングとキャプチャのエンドポイントが含まれています。
ms.assetid: 4F163A65-5572-41D0-80B2-493285E2B87B
keywords:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 943bb388dad81319c759c8031b54536e47c7849b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558637"
---
# <a name="kspropertytelephonyendpointidpair"></a>KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR


**KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR**プロパティに携帯電話の音声ルーティングのレンダリングとキャプチャのエンドポイントが含まれています。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169887" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTIDPAIR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169887)"><strong>KSTOPOLOGY_ENDPOINTIDPAIR</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型[ **KSTOPOLOGY\_ENDPOINTIDPAIR**](https://msdn.microsoft.com/library/windows/hardware/mt169887)レンダリングとキャプチャのエンドポイントを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR**プロパティ要求は、携帯電話の音声ルーティングのレンダリングとキャプチャのエンドポイントを返します。

<a name="remarks"></a>注釈
-------

携帯電話ルーティングによって制御されます**KSPROPERTY\_テレフォニー\_ENDPOINTIDPAIR**トポロジ フィルターのプロパティ。 このプロパティは 1 組の[ **KSTOPOLOGY\_ENDPOINTID** ](https://msdn.microsoft.com/library/windows/hardware/mt169886)構造体が要求されたエンドポイントの組み合わせ。 **KSTOPOLOGY\_ENDPOINTID**エンドポイントとエンドポイントが接続されているトポロジ フィルター pin ID トポロジ フィルターの参照文字列が含まれています。 ドライバーは、このプロパティの基本的なサポートを提供し、すべてのレンダーの有効なペアを返しますおよび携帯電話の音声ルーティングのために使用できるエンドポイントをキャプチャします。 表示し、この新しいエンドポイントの組み合わせ、どのような制約は、ハードウェアに必要な会議を携帯電話のオーディオのキャプチャの両方の移動を処理するために、ドライバーの役目です。 このプロパティは、システムでアクティブな電話呼び出しがない場合でも、設定可能にする必要があります。

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

 

 





