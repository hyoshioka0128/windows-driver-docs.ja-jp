---
title: KSPROPERTY\_オーディオ\_MUX\_ソース
description: KSPROPERTY\_オーディオ\_MUX\_ソース プロパティは、マルチプレクサーの出力ストリームのソースを指定します。 これは、MUX ノードのプロパティ (KSNODETYPE\_MUX)。
ms.assetid: 631d12f2-3f30-4d3e-a0b2-731634858897
keywords:
- KSPROPERTY_AUDIO_MUX_SOURCE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MUX_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8454969ac993c5dbb9d41526bc920688aa37109c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551694"
---
# <a name="kspropertyaudiomuxsource"></a>KSPROPERTY\_オーディオ\_MUX\_ソース


KSPROPERTY\_オーディオ\_MUX\_ソース プロパティは、マルチプレクサーの出力ストリームのソースを指定します。 これは、MUX ノードのプロパティ ([**KSNODETYPE\_MUX**](ksnodetype-mux.md))。

## <span id="ddk_ksproperty_audio_mux_source_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MUX_SOURCE_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は、ULONG 型です。 この値は、MUX ノードで選択した入力ピンの暗証番号 (pin) の ID です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_MUX\_ソース プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

暗証番号 (pin) の ID は、MUX ノード上の論理ピンを識別します。 フィルター内のノードの論理ピンの暗証番号 (pin) の Id の詳細については、次を参照してください。 [ **PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_MUX**](ksnodetype-mux.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)

 

 






