---
title: KSPROPERTY\_オーディオ\_MIC\_SNR
description: KSPROPERTY\_オーディオ\_MIC\_SNR プロパティは、マイクの信号雑音比 (SNR) dB 単位で測定するを指定します。
ms.assetid: 1DF088D0-7C0D-42B6-B7FA-2E714C70DAA4
keywords:
- KSPROPERTY_AUDIO_MIC_SNR オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SNR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80a0f799b700ba800e97b4d16372e16c36d742f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553200"
---
# <a name="kspropertyaudiomicsnr"></a>KSPROPERTY\_オーディオ\_MIC\_SNR


KSPROPERTY\_オーディオ\_MIC\_SNR プロパティは、マイクの信号雑音比 (SNR) dB 単位で測定するを指定します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

使用状況の概要テーブル

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

 

プロパティ値 (データの操作) は LONG 型の dB 単位 SNR 情報が含まれます。 値には、固定小数点 10 進表記が使用されます。 データは、16.16 固定小数点値として格納されます。 値の整数の上位 16 ビットを使用し、値の小数部の下位 16 ビットを使用します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_MIC\_SNR プロパティ要求がステータスを返す\_要求が正常に完了すると成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオ ドライバーには、それぞれのマイクのマイク SNR を取得できます。 このプロパティは、ドライバーから取得するには、この情報を使用します。

音声認識エクスペリエンスを Windows 10 を正確に検出し、さまざまなデバイスでユーザーの音声を別のマイクと分析、Cortana など、OS は、入力信号の特定の特性を把握する必要があります。 その情報に基づいて、OS は有効な秘密度を計算し、入力信号を強化するために適切な向上を適用します。 詳細については、[音声をアクティブ化](https://msdn.microsoft.com/library/windows/hardware/mt593238)を参照してください。

KSPROPERTY\_オーディオ\_MIC\_SNR は Windows 10 バージョン 1607 以降を使用できます。

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

 

 





