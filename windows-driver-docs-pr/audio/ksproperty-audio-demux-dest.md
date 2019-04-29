---
title: KSPROPERTY\_オーディオ\_DEMUX\_DEST
description: KSPROPERTY\_オーディオ\_DEMUX\_DEST プロパティをデマルチプレクサーがその入力ストリームを送信する先のストリームを指定します。 これは、プロパティは DEMUX ノードのプロパティ (KSNODETYPE\_DEMUX)。
ms.assetid: 431918da-2267-4fe5-a002-12d16b5f0984
keywords:
- KSPROPERTY_AUDIO_DEMUX_DEST オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DEMUX_DEST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 700d9fba987521ff11af671b948890385d104acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333064"
---
# <a name="kspropertyaudiodemuxdest"></a>KSPROPERTY\_オーディオ\_DEMUX\_DEST


KSPROPERTY\_オーディオ\_DEMUX\_DEST プロパティをデマルチプレクサーがその入力ストリームを送信する先のストリームを指定します。 これは、プロパティは DEMUX ノードのプロパティ ([**KSNODETYPE\_DEMUX**](ksnodetype-demux.md))。

## <span id="ddk_ksproperty_audio_demux_dest_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEMUX_DEST_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は、ULONG 型です。 この値は DEMUX ノードで選択した出力ピンの暗証番号 (pin) の ID です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_DEMUX\_DEST プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

暗証番号 (pin) の ID では、論理ピン DEMUX ノードで識別します。 フィルター内のノードの論理ピンの暗証番号 (pin) の Id の詳細については、次を参照してください。 [ **PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)します。

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


[**KSNODETYPE\_DEMUX**](ksnodetype-demux.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)

 

 






