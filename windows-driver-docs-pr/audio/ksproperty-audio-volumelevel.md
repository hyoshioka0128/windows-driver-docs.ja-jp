---
title: KSPROPERTY\_オーディオ\_VOLUMELEVEL
description: KSPROPERTY\_オーディオ\_VOLUMELEVEL プロパティは、[ボリューム] ノードで、チャネルのボリューム レベルを指定します (KSNODETYPE\_ボリューム)。
ms.assetid: 5b420c71-fc82-413d-a93d-e8f3408cc8d7
keywords:
- KSPROPERTY_AUDIO_VOLUMELEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af23b51c9564f0ca63bc4a2e3fb9701d683b9f72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332928"
---
# <a name="kspropertyaudiovolumelevel"></a>KSPROPERTY\_オーディオ\_VOLUMELEVEL


KSPROPERTY\_オーディオ\_VOLUMELEVEL プロパティは、[ボリューム] ノードで、チャネルのボリューム レベルを指定します ([**KSNODETYPE\_ボリューム**](ksnodetype-volume.md))。

## <span id="ddk_ksproperty_audio_volumelevel_ks"></span><span id="DDK_KSPROPERTY_AUDIO_VOLUMELEVEL_KS"></span>


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
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルターまたは暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は LONG 型の指定したストリームのチャネルのボリューム レベルを指定します。 ボリューム レベルの値は、次のスケールを使用します。

無限大デシベル (減衰) は-2147483648

-2147483647 は-32767.99998474 デシベル (減衰) と

+ 2147483647 までは、+32767.99998474 デシベル (向上です)。

&gt; \[!注\] &gt; + 2147483647 まで、このスケールが 1/65536 デシベルの解像度を-2147483648 から、デシベル範囲が整数値で表されます。

 

フィルターの範囲を超える値を指定すると、このプロパティを設定する要求は引き続き成功します。 フィルターが適用された実際の値を決定のみできますが、このプロパティへの後続の Get 呼び出しで。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_VOLUMELEVEL プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

このプロパティのプロパティ記述子には、チャンネル番号を指定します。 [ボリューム] ノードを通過するストリームを含むかどうか*n*チャネル、チャネルは番号が 0 ~ *n*-1。 詳細については、次を参照してください。[マルチ チャネルのノードを公開する](https://msdn.microsoft.com/library/windows/hardware/ff536380)します。

<a name="requirements"></a>必要条件
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


[既定のオーディオ音量設定のカスタマイズ](https://msdn.microsoft.com/library/windows/hardware/jj870738)

[既定のオーディオの音量の設定](https://msdn.microsoft.com/library/windows/hardware/ff536251)

[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)

 

 






