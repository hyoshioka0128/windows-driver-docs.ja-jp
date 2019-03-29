---
title: KSPROPERTY\_オーディオ\_バッファー\_期間
description: KSPROPERTY\_オーディオ\_バッファー\_期間プロパティは、期間として報告されることをクライアント アプリケーションのバッファーのサイズを使用します。
ms.assetid: 9749464f-d351-468b-b785-fa84705ef2c0
keywords:
- KSPROPERTY_AUDIO_BUFFER_DURATION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BUFFER_DURATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749bbdc6239b9b986303523494aea91bc1568eec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574553"
---
# <a name="kspropertyaudiobufferduration"></a>KSPROPERTY\_オーディオ\_バッファー\_期間


KSPROPERTY\_オーディオ\_バッファー\_期間プロパティは、期間として報告されることをクライアント アプリケーションのバッファーのサイズを使用します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は ULONG 型で、ミリ秒単位で測定されるクライアント バッファー期間を表します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_バッファー\_期間プロパティ要求がステータスを返します\_プロパティ要求が正常に完了したことを示す成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

USB オーディオ デバイスのパフォーマンスを向上させるアイソクロナスのオーディオ データのキャプチャ要求の期間を調整することができます。 期間を短くは待機時間を削減しますが、USB オーディオ スタックがパフォーマンスの低下を引き起こす可能性がありますより頻繁に遅延プロシージャ呼び出し (DPC) を行う必要がありますも意味します。

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
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





