---
title: KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2
description: KSPROPERTY_AUDIO_MIC_SENSITIVITY プロパティは、マイクの感度をハードウェア利点を得ることなどのフル スケール (dBFS) ユニットの基準としたデシベル単位で指定します。
keywords:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY2 オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: ceb3f629202e768ca1c013d853494c38120ca183
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333010"
---
# <a name="kspropertyaudiomicsensitivity2"></a>KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2

KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2 プロパティは、マイクの感度をハードウェア利点を得ることなどのフル スケール (dBFS) ユニットの基準としたデシベル単位を指定します。 この値には、ソフトウェア利点を得ることの前に、mic の秘密度に影響を与える、ハードウェアの統合が含まれています。  KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2 プロパティは、オーディオ スタックから適用されるソフトウェア利点を得ることは含まれません。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>取得</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>対象</p></td>
<td align="left"><p>プロパティ記述子の型</p></td>
<td align="left"><p>プロパティ値の型</p></td>
</tr>
<tr class="even">
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>暗証番号 (pin) のインスタンス</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></td>
<td align="left">LONG</td>
</tr>
</tbody>
</table>

プロパティ値 (データの操作) は LONG 型の dBFS ユニットの基準としたデシベル単位での区別に関する情報が含まれています。 感度値では、次のスケールを使用します。 値には、固定小数点 10 進表記が使用されます。 データは、16.16 固定小数点値として格納されます。 値の整数の上位 16 ビットを使用し、値の小数部の下位 16 ビットを使用します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2 プロパティ要求がステータスを返す\_要求が正常に完了すると成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオ ドライバーには、それぞれのマイクのマイクの感度を取得できます。 このプロパティは、ドライバーから取得するには、この情報を使用します。

Cortana などの Windows 10 音声認識エクスペリエンスを正確に検出し、別のマイクを使用したさまざまなデバイスでユーザーのボイスの分析、OS 必要があります、入力信号の特定の特性を把握します。 その情報に基づいて、OS は有効な秘密度を計算し、入力信号を強化するために適切な向上を適用します。 詳細については、次を参照してください。[音声をアクティブ化](https://msdn.microsoft.com/library/windows/hardware/mt593238)します。

KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2 は以降 Windows 10 バージョン 1803 で利用可能よりも優先されます[KSPROPERTY\_オーディオ\_MIC\_の感度](ksproperty-audio-mic-sensitivity.md).


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

<a name="see-also"></a>関連項目
---------

[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)





