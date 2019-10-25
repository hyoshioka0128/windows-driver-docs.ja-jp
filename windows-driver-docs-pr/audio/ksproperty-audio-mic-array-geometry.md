---
title: KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY
description: KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY プロパティは、マイク配列のジオメトリを指定します。
ms.assetid: c9153c65-06d1-4968-8d70-64aafc760a8c
keywords:
- KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f1e1db82cdbe18ab0f0bb101b86bb209aeafbde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832996"
---
# <a name="ksproperty_audio_mic_array_geometry"></a>KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY


KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY プロパティは、マイク配列のジオメトリを指定します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は KSK AUDIO\_MIC\_配列\_GEOMETRY です。 詳細については、 [**Ksk audio\_MIC\_配列\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)構造体の定義を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY プロパティ要求は、要求が正常に完了した時点で成功\_状態を返します。

[**KSP\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造体の pinid メンバーによって示された pin が mic 配列要求をサポートしていない場合、プロパティ要求はステータス\_返され\_サポートされません。

要求のバッファーサイズが0に設定されている場合、プロパティ要求は、状態\_バッファー\_オーバーフロー状態を返します。 さらに、この要求では、リターンステータスブロックを使用して、pin によってサポートされている KSK オーディオ\_MIC\_配列\_のサイズを示します。

要求のバッファーサイズが、返された構造に合わせて小さすぎるバッファーサイズに設定されている場合、要求は状態\_バッファーの状態を返し\_\_小さすぎます。 次に、この要求では、リターンステータスブロックを使用して、pin によってサポートされている[**Ksk オーディオ\_MIC\_配列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)のサイズを示します。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_AUDIO\_MIC\_配列\_GEOMETRY プロパティでサポートされるのは、KSK プロパティ\_GET 要求だけです。 クライアントが geometry 構造全体を格納するために必要なバッファーの正しいサイズを判断するためには、最初に要求のバッファーサイズをゼロに設定する必要があります。 クライアントは、status ブロックで返された値を使用してバッファーサイズを正しく設定した後、適切なサイズのバッファーで別のプロパティ要求を行うことができます。

Windows でマイクアレイを処理する方法の詳細については、次のリソースを参照してください。

[Windows でのマイク配列のサポート (ホワイトペーパー)](https://go.microsoft.com/fwlink/p/?linkid=120592)

[マイク配列の Geometry プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/microphone-array-geometry-property)

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIO\_MIC\_配列\_GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






