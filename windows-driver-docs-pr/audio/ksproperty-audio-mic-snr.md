---
title: KSK プロパティ\_AUDIO\_MIC\_SNR
description: KSK プロパティ\_AUDIO\_MIC\_SNR プロパティは、dB ユニットで測定されたマイク信号 (SNR) を指定します。
ms.assetid: 1DF088D0-7C0D-42B6-B7FA-2E714C70DAA4
keywords:
- KSPROPERTY_AUDIO_MIC_SNR オーディオデバイス
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
ms.openlocfilehash: 07205df06e192a4f92b583097986aa0df7dd97e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831034"
---
# <a name="ksproperty_audio_mic_snr"></a>KSK プロパティ\_AUDIO\_MIC\_SNR


KSK プロパティ\_AUDIO\_MIC\_SNR プロパティは、dB ユニットで測定されたマイク信号 (SNR) を指定します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<td align="left"><p>[購入]</p></td>
<td align="left"><p>設定</p></td>
<td align="left"><p>対象</p></td>
<td align="left"><p>プロパティ記述子の型</p></td>
<td align="left"><p>プロパティ値の型</p></td>
</tr>
<tr class="even">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>インスタンスのピン留め</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left">長い</td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は LONG 型で、dB 単位に SNR 情報が含まれています。 この値は、固定小数点の10進数表現を使用します。 データは16.16 固定ポイント値として格納されます。 上位16ビットは値の整数に使用され、下位16ビットは値の小数部分に使用されます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_MIC\_SNR プロパティ要求は、要求が正常に完了したときに成功\_状態を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオドライバーは、各マイクのマイク SNR を取得できます。 このプロパティを使用すると、この情報をドライバーから取得できます。

Cortana などの Windows 10 の音声認識エクスペリエンスで、さまざまなデバイスのマイクを使用してユーザーの音声を正確に検出して分析するには、OS が入力信号の特定の特性を認識している必要があります。 OS は、この情報に基づいて、有効な感度を計算し、適切なゲインを適用して入力信号を強化できます。 詳細については、「[音声ライセンス認証](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)」を参照してください。

KSK プロパティ\_AUDIO\_MIC\_SNR は、Windows 10 バージョン1607以降で使用できます。

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
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

 

 





