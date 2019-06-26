---
title: KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL
description: KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL プロパティで指定したストリーム チャネルのボリューム レベルを指定します。
ms.assetid: E10E2ADC-BD76-4871-85DA-19385A0D77EE
keywords:
- KSPROPERTY_AUDIOENGINE_VOLUMELEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7efaf513f0408f8ad842022988f130a95bca57d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358833"
---
# <a name="kspropertyaudioenginevolumelevel"></a>KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL


**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**プロパティで指定したストリーム チャネルのボリューム レベルを指定します。

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
<td align="left"><p>暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>時間の長い (Get 要求) 用と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_VOLUMELEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)"> <strong>KSAUDIOENGINE_VOLUMELEVEL</strong> </a> (用セットの要求)。</p></td>
</tr>
</tbody>
</table>

 

プロパティの値が LONG 型では Get 要求とでのチャネルのボリューム レベルを指定します、ストリームを指定します。 ボリューム レベルの値は、以下のスケールを使用して、このプロパティの基本的なサポートの応答で指定された最小値と最大値を区切る。

-2147483648 (16 進数、または時間の長い 0x80000000\_MIN) は、無限大デシベル (減衰)

-2147483647 (16 進数、または時間の長い 0x80000001\_分 + 1) は-32767.99998474 デシベル (減衰) と

\+ 2147483647 まで (16 進数、または時間の長い 0x7FFFFFFF\_MAX) は +32767.99998474 デシベル (向上)。

&gt; \[!注\] &gt; + 2147483647 まで、このスケールが 1/65536 デシベルの解像度を-2147483648 から、デシベル範囲が整数値で表されます。

 

プロパティの値はセットの要求の種類の**KSAUDIOENGINE\_VOLUMELEVEL**、および、ボリュームとして適用する曲線と曲線の型期間と同様に、指定したストリームでチャネルの適切なボリューム レベルを指定しますレベルが設定されています。 フィルターの範囲を超える値を指定すると、このプロパティを設定する要求は引き続き成功します。 フィルターが適用された実際の値を決定のみできますが、このプロパティへの後続の Get 呼び出しで。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

[ **KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS** ](ksproperty-audioengine-supporteddeviceformats.md)プロパティ要求を返します**状態\_成功**に正常に完了したことを示します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

プロパティ記述子を**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**チャンネル番号を指定します。 オーディオ エンジン ノードを通過するストリームを含むかどうか*n*チャネル、チャネルは番号が 0 ~ *n-1*します。 0 xffffffff のチャネルの値が、要求がすべてのチャネルに適用されることを示すことに注意してください。 ストリームが実行状態にないときにプロパティの要求が行われた場合、ボリューム レベルは、要求されたレベルにすぐに設定されます。 ボリューム レベルのランプが進行中は実行状態のまま、ストリーム場合、ストリームのボリューム レベルはすぐに現在フェードのターゲット レベルに設定します。 既存のボリューム レベル ランプが進行中はプロパティの新しい要求が行われた場合、新しいごとの傾斜増加要求は、現在ボリューム レベルの新しい要求を受信したときに、ボリュームの限界に到達するレベルから始める必要があります。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSAUDIOENGINE\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

 

 






