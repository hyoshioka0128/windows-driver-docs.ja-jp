---
title: KSK プロパティ \_ AUDIOENGINE \_ VOLUMELEVEL
description: KSK プロパティ \_ audioengine \_ VOLUMELEVEL プロパティは、指定されたストリームのチャネルのボリュームレベルを指定します。
ms.assetid: E10E2ADC-BD76-4871-85DA-19385A0D77EE
keywords:
- KSPROPERTY_AUDIOENGINE_VOLUMELEVEL オーディオデバイス
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
ms.openlocfilehash: de2d9c1e8892beac80accb748d24ab35a63205f5
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851309"
---
# <a name="ksproperty_audioengine_volumelevel"></a>KSK プロパティ \_ AUDIOENGINE \_ VOLUMELEVEL


**Ksk プロパティ \_ audioengine \_ VOLUMELEVEL**プロパティは、指定されたストリームのチャネルのボリュームレベルを指定します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">オン</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>ピンのインスタンスによるノード</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>LONG (Get 要求の場合) と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_VOLUMELEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)"><strong>KSAUDIOENGINE_VOLUMELEVEL</strong></a> (セット要求の場合)。</p></td>
</tr>
</tbody>
</table>

 

Get 要求の場合、プロパティ値は LONG 型で、指定されたストリームのチャネルのボリュームレベルを指定します。 ボリュームレベルの値は、次のスケールを使用します。このプロパティの基本サポート応答に指定されている最小値と最大値によって制限できます。

-2147483648 (16 進数の0x80000000、または LONG \_ MIN) は-無限大デシベル (減衰) です。

-2147483647 (16 進数の0x80000001、または LONG \_ MIN + 1) は-32767.99998474 デシベル (減衰)、および

+ 2147483647 (16 進数の0x7FFFFFFF、または長い \_ 最大値) は + 32767.99998474 デシベル (ゲイン) です。

> [!NOTE]
> デシベル範囲は、-2147483648 ~ + 2147483647 の整数値によって表されます。このスケールでは、1/65536 デシベルが解決されます。

 

Set 要求の場合、プロパティ値は**KSAUDIOENGINE \_ VOLUMELEVEL**型で、指定されたストリームのチャネルの望ましいボリュームレベル、およびボリュームレベルが設定されているときに適用される曲線の種類と曲線の期間を指定します。 値がフィルターの範囲を超えて指定されている場合でも、このプロパティを設定する要求は成功します。 ただし、フィルターに適用された実際の値は、このプロパティの後続の Get 呼び出しによってのみ決定できます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

[**Ksk プロパティ \_ audioengine \_ supporteddeviceformats**](ksproperty-audioengine-supporteddeviceformats.md)プロパティ要求は、正常に完了したことを示す**ステータス \_ 成功**を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

**Ksk プロパティ \_ audioengine \_ VOLUMELEVEL**のプロパティ記述子は、チャネル番号を指定します。 オーディオエンジンノードを通過するストリームに*n 個*のチャネルが含まれている場合、チャネルには0から*n-1*までの番号が付けられます。 また、チャネル値0xFFFFFFFF は、要求がすべてのチャネルに適用されることを示します。 ストリームが実行中の状態でないときにプロパティ要求が行われた場合、ボリュームレベルは直ちに要求されたレベルに設定されます。 ボリュームレベルの傾斜が進行しているときにストリームが実行状態を離れると、ストリームのボリュームレベルは、現在のフェードのターゲットレベルに直ちに設定されます。 既存のボリュームレベルの傾斜が進行している間に新しいプロパティ要求が行われた場合、新しい傾斜要求は、現在のボリュームレベル (新しい要求が到着したときにボリュームが到達したレベル) から開始する必要があります。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIOENGINE \_ VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_volumelevel)

[**KSNODEPROPERTY \_ オーディオ \_ チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSK プロパティ \_ AUDIOENGINE**](ksproperty-audioengine.md)

[**KSK プロパティ \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

 

 






