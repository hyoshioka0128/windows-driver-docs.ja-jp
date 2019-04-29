---
title: KSPROPERTY\_オーディオ\_優先\_状態
description: KSPROPERTY\_オーディオ\_優先\_STATUS プロパティは、システムの優先するオーディオ デバイスであるをデバイスに通知します。
ms.assetid: a0e89143-ead1-4e0d-a550-398ec1abf9e9
keywords:
- KSPROPERTY_AUDIO_PREFERRED_STATUS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PREFERRED_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2bcbcf8f0facc1830f7d3309fcc2c482237086a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332949"
---
# <a name="kspropertyaudiopreferredstatus"></a>KSPROPERTY\_オーディオ\_優先\_状態


KSPROPERTY\_オーディオ\_優先\_STATUS プロパティは、システムの優先するオーディオ デバイスであるをデバイスに通知します。

## <span id="ddk_ksproperty_audio_preferred_status_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PREFERRED_STATUS_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537093" data-raw-source="[&lt;strong&gt;KSAUDIO_PREFERRED_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537093)"><strong>KSAUDIO_PREFERRED_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_優先\_そのデバイスの種類には、好みのデバイスとしての種類は好みのデバイスとデバイスを選択または選択解除するかどうかを示す状態。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_優先\_プロパティの状態要求のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

[SysAudio システム ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver) wave レコード、MIDI、またはミキサーのデバイスを優先する新しいデバイスを選択したとき、または以前に選択したときに優先するデバイスの選択を解除ウェーブの再生を通知するためにこのプロパティを使用します。

任意のデバイスについては、次を参照してください。 [ **SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)します。

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

[**KSAUDIO\_優先\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff537093)

[**SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)

 

 






