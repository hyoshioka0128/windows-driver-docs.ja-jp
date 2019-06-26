---
title: KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置
description: KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置プロパティ要求では、現在では、WaveRT バッファーの位置を書き込む (バイト単位) を指定します。 オフロード ドライバーでは、WaveRT バッファーで有効なデータの量を把握するのにこの書き込み位置情報を使用できます。
ms.assetid: 05C62E23-2460-4E92-BEE8-08D31A8BFD86
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c7dd2b4d0735c79cddb737f79fe060b7a7f237a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360568"
---
# <a name="kspropertyaudiowavertcurrentwriteposition"></a>KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置


KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置プロパティ要求では、現在では、WaveRT バッファーの位置を書き込む (バイト単位) を指定します。 オフロード ドライバーでは、WaveRT バッファーで有効なデータの量を把握するのにこの書き込み位置情報を使用できます。

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
<td align="left"><p>暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティの要求によって提供された情報を解釈する方法を理解するには、サイズが n バイトの循環バッファーを想定しています。 すべてのデータが書き込まれる前に、初期の書き込み位置には 0 です。 倍数であるチャンク バッファーにデータが書き込まれる[ **WAVEFORMATEX.nBlockAlign** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)バイト。

たとえば、バッファーには、20 ミリ秒 48000 Hz のサンプリングされた 16 ビット PCM ステレオ データにはが含まれます。 NBlockAlign メンバーの説明に基づいて、 **WAVEFORMATEX**構造体の場合は、この例の nBlockAlign で、2 = \* 16/8 = 4 バイト。 つまり、バッファーの長さが 48000 である\*20/1000 = 960 のフレームまたは 960 \* 4 = 3840 バイト。

最初の**設定**要求は、バッファーに書き込まれたバイト数を指定します。 3840 の値がいっぱいバッファー サイズを示す場合は、1920 年の値がバッファー サイズの半分を指定はため、「書き込み位置」は、バイト単位で表現は、します。 以降を行うため、書き込まれた新しいバイト数を決定する**設定**要求すると、次の擬似コードは、計算を実行する方法を示します。

``` syntax
if new write position > old write position:
     bytes written = new write position – old write position
if new write position < old write position, we’ve wrapped:
     bytes written = (new write position + buffer size) – old write position
if new write position = old write position, we’ve had a glitch
     log a "duplicate write position" glitch event
```

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


[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)

 

 






