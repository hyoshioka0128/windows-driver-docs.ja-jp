---
title: KSPROPERTY\_SYSAUDIO\_選択\_グラフ
description: KSPROPERTY\_SYSAUDIO\_選択\_SysAudio が仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスの構築をグラフに省略可能なノードを明示的に含めるグラフ プロパティを使用します。
ms.assetid: 1107e20e-9ba8-4fda-8457-c357426a9cda
keywords:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79eb872c3761d483363c0eafd960cd662982c1c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539333"
---
# <a name="kspropertysysaudioselectgraph"></a>KSPROPERTY\_SYSAUDIO\_選択\_グラフ


KSPROPERTY\_SYSAUDIO\_選択\_SysAudio が仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスの構築をグラフに省略可能なノードを明示的に含めるグラフ プロパティを使用します。

## <span id="ddk_ksproperty_sysaudio_select_graph_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_SELECT_GRAPH_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538500" data-raw-source="[&lt;strong&gt;SYSAUDIO_SELECT_GRAPH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538500)"><strong>SYSAUDIO_SELECT_GRAPH</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、型 SYSAUDIO の構造\_選択\_プロパティ、暗証番号 (pin) の ID、およびノードの ID を示すグラフ プロパティが型の埋め込み構造体で指定された[ **KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)します。 暗証番号 (pin) の ID は、仮想のオーディオ デバイスをラップする KS フィルターでピン留めするファクトリを識別するインデックスです。 ノード ID は、指定した pin のデータ パス内の省略可能なノードを識別するインデックスです。 詳細については、次の「解説」を参照してください。

このプロパティのプロパティの値 (データの操作) が定義されていません。 プロパティ値のバッファーのポインターとして指定**NULL**とそのサイズを 0 として。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_選択\_GRAPH プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、AEC のノードを強制的に暗証番号 (pin) のインスタンスのグラフに通常使用されます。

仮想デバイスのオーディオ フィルターでレンダリング暗証番号 (pin) をインスタンス化するときに、SysAudio は、暗証番号 (pin) から開始し、既定でフィルターを最も簡単なパスを表すグラフを選択します。 このグラフは、AEC コントロールなどの任意の省略可能なノードを除外します。

最初の送信 SysAudio、KSPROPERTY SysAudio の既定の動作をオーバーライドする\_SYSAUDIO\_選択\_グラフ内に含まれるオプションのノードを指定するグラフ プロパティの設定要求。 SysAudio は、その後、暗証番号 (pin) のインスタンスを作成するとき、暗証番号 (pin) のグラフは、要求で指定されたオプションのノードが含まれます。

KSPROPERTY\_SYSAUDIO\_選択\_グラフ プロパティの設定要求の要求の後に作成されている暗証番号 (pin) インスタンスのみに影響を与えます。 要求は、以前にインスタンス化されたピンへの影響を与えません。

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


[**SYSAUDIO\_選択\_グラフ**](https://msdn.microsoft.com/library/windows/hardware/ff538500)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






