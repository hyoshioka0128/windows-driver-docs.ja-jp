---
title: KSPROPERTY\_オーディオ\_待機時間
description: KSPROPERTY\_オーディオ\_遅延 (またはオーディオのバッファー量) をレポートに待機時間のプロパティを使用したストリームに関連付けられています。
ms.assetid: d155e3a5-e3e6-4381-9bbe-2a16b0be47b3
keywords:
- KSPROPERTY_AUDIO_LATENCY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e171287ffb0ad9a0e1dd3ccb04cadda5c00481
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333024"
---
# <a name="kspropertyaudiolatency"></a>KSPROPERTY\_オーディオ\_待機時間


KSPROPERTY\_オーディオ\_遅延 (またはオーディオのバッファー量) をレポートに待機時間のプロパティを使用したストリームに関連付けられています。

## <span id="ddk_ksproperty_audio_latency_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LATENCY_KS"></span>


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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567145" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567145)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ストリームの待機時間を指定する KSTIME 型の構造です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_プロパティ要求の待機時間のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、AEC のフィルターを 暗証番号 (pin) のストリームの待機時間をクエリに使用されます。 詳細については、次を参照してください。 [Exposing Hardware-Accelerated キャプチャ効果](https://msdn.microsoft.com/library/windows/hardware/ff536379)します。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSTIME**](https://msdn.microsoft.com/library/windows/hardware/ff567145)

 

 






