---
title: KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2
description: KSPROPERTY_AUDIO_MIC_SENSITIVITY プロパティは、ハードウェアの利益を含め、フルスケール (dBFS) ユニットを基準としたマイクの感度をデシベル単位で指定します。
keywords:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY2 オーディオデバイス
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
ms.openlocfilehash: 0bd5321612badb5977a6e286ba3853d4acfe2689
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832981"
---
# <a name="ksproperty_audio_mic_sensitivity2"></a>KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2

KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2 プロパティは、ハードウェアの利益を含め、フルスケール (dBFS) ユニットを基準とするマイクの感度をデシベル単位で指定します。 この値には、ソフトウェアが利用できるようになる前に、マイクの感度に影響を与えるハードウェアの統合が含まれます。  KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2 プロパティには、オーディオスタックから適用されるソフトウェアゲインは含まれていません。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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

プロパティ値 (操作データ) は LONG 型で、dBFS unit を基準とした相対的な値がデシベル単位で格納されます。 秘密度の値には、次のスケールが使用されます。 この値は、固定小数点の10進数表現を使用します。 データは16.16 固定ポイント値として格納されます。 上位16ビットは値の整数に使用され、下位16ビットは値の小数部分に使用されます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2 property 要求は、要求が正常に完了したときに成功\_状態を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオドライバーは、各マイクのマイクの感度を取得できます。 このプロパティを使用すると、この情報をドライバーから取得できます。

Cortana などの Windows 10 の音声認識エクスペリエンスで、さまざまなマイクを持つさまざまなデバイスでユーザーの音声を正確に検出して分析するには、OS が入力信号の特定の特性を認識している必要があります。 OS は、この情報に基づいて、有効な感度を計算し、適切なゲインを適用して入力信号を拡張できます。 詳細については、「[音声ライセンス認証](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)」を参照してください。

KSK プロパティ\_AUDIO\_MIC\_SENSITIVITY2 は、Windows 10 バージョン1803以降で使用可能であり、 [Ksk プロパティ\_audio\_MIC\_の秘密度](ksproperty-audio-mic-sensitivity.md)に優先します。


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

<a name="see-also"></a>参照
---------

[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)





