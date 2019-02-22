---
title: KSPROPERTY\_オーディオ\_MIC\_と小文字の区別
description: KSPROPERTY\_オーディオ\_MIC\_感度プロパティは、マイクの感度をフル スケール (dBFS) ユニットの基準としたデシベル単位を指定します。
ms.assetid: FE62AAA5-E022-459F-817B-3661535FA9BD
keywords:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c82f8d5231c6ae66c690c33cd7772a6080358d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539328"
---
# <a name="kspropertyaudiomicsensitivity"></a>KSPROPERTY\_オーディオ\_MIC\_と小文字の区別

KSPROPERTY\_オーディオ\_MIC\_感度プロパティは、マイクの感度をフル スケール (dBFS) ユニットの基準としたデシベル単位を指定します。

> [!NOTE]
> KSPROPERTY\_オーディオ\_MIC\_と小文字の区別は Windows 10 バージョン 1803 以降非推奨とされます。 使用[KSPROPERTY\_オーディオ\_MIC\_SENSITIVITY2](ksproperty-audio-mic-sensitivity2.md)代わりにします。

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
<td align="left">長い</td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は LONG 型の dBFS ユニットの基準としたデシベル単位での区別に関する情報が含まれています。 感度値では、次のスケールを使用します。 値には、固定小数点 10 進表記が使用されます。 データは、16.16 固定小数点値として格納されます。 値の整数の上位 16 ビットを使用し、値の小数部の下位 16 ビットを使用します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_MIC\_感度プロパティ要求がステータスを返す\_要求が正常に完了すると成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオ ドライバーには、それぞれのマイクのマイクの感度を取得できます。 このプロパティは、ドライバーから取得するには、この情報を使用します。

音声認識エクスペリエンスを Windows 10 を正確に検出し、さまざまなデバイスでユーザーの音声を別のマイクと分析、Cortana など、OS は、入力信号の特定の特性を把握する必要があります。 その情報に基づいて、OS は有効な秘密度を計算し、入力信号を強化するために適切な向上を適用します。 詳細については、次を参照してください。[音声をアクティブ化](https://msdn.microsoft.com/library/windows/hardware/mt593238)します。

KSPROPERTY\_オーディオ\_MIC\_と小文字の区別は、Windows 10 バージョン 1607 以降を使用できます。

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

 

 





