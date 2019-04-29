---
title: KSPROPERTY\_オーディオ\_PEAKMETER
description: KSPROPERTY\_オーディオ\_PEAKMETER プロパティ peakmeter ノードで発生したオーディオ信号の最大レベルを取得します (KSNODETYPE\_PEAKMETER) peakmeter ノードの前回がリセットされました。
ms.assetid: c8c2c9ed-61ea-4bbe-b376-c956f051416e
keywords:
- KSPROPERTY_AUDIO_PEAKMETER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437d24da91f7fb3f40f12b13e5529c8de35797e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332917"
---
# <a name="kspropertyaudiopeakmeter"></a>KSPROPERTY\_オーディオ\_PEAKMETER


KSPROPERTY\_オーディオ\_PEAKMETER プロパティ peakmeter ノードで発生したオーディオ信号の最大レベルを取得します ([**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md))最後に、peakmeter ノードがリセットされました。

## <span id="ddk_ksproperty_audio_peakmeter_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER_KS"></span>


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
<td align="left"><p>フィルターまたは暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型のノードでピーク時のサンプル値を指定します。 ピーク時の値が負の場合は、その絶対値が使用します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_PEAKMETER プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、考えられるエラーの状態コードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>KS フィルターは、peakmeter の現在の値を返すことはできません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ フィルターは、このプロパティの要求を同期的に処理します。 要求が成功した場合は、累積最大値をゼロに初期化すると、peakmeter がリセットされます。 要求が成功しなかった場合、peakmeter は変更されません。

システムは、IOCTL、送信\_KS\_プロパティ要求、KSPROPERTY\_オーディオ\_IRQL パッシブ PEAKMETER プロパティ\_レベル。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






