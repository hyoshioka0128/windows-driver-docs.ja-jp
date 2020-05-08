---
title: KSK プロパティ\_オーディオ\_MIC\_配列\_ジオメトリ
description: KSK プロパティ\_の AUDIO\_MIC\_配列\_ジオメトリプロパティは、マイク配列のジオメトリを指定します。
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
ms.openlocfilehash: bcfc821fa11245addbae124bb2f289a95366afd6
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925593"
---
# <a name="ksproperty_audio_mic_array_geometry"></a>KSK プロパティ\_オーディオ\_MIC\_配列\_ジオメトリ


KSK プロパティ\_の AUDIO\_MIC\_配列\_ジオメトリプロパティは、マイク配列のジオメトリを指定します。

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
<td align="left"><p>取得</p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>移行先</p></td>
<td align="left"><p>プロパティ記述子の型</p></td>
<td align="left"><p>プロパティ値の型</p></td>
</tr>
<tr class="even">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Assert</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は KSK AUDIO\_MIC\_配列\_GEOMETRY です。 詳細については、 [**\_ksaudio\_MIC\_配列 GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)構造体の定義を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_Ksk プロパティの AUDIO\_MIC\_配列\_GEOMETRY プロパティ要求は、要求\_が正常に完了した時点で成功状態を返します。

[**KSP\_のピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造の pinid メンバーによって示された pin が mic 配列要求をサポートしていない場合、プロパティ\_要求\_はサポートされていない状態を返します。

要求のバッファーサイズが0に設定されている場合、プロパティ要求はステータス\_バッファー\_のオーバーフロー状態を返します。 さらに、この要求では、リターンステータスブロックを使用して、ピンで\_サポート\_さ\_れている ksk オーディオ MIC 配列の GEOMETRY 構造体のサイズを示します。

要求のバッファーサイズが、返された構造に合わせて小さすぎるバッファーサイズに設定されている場合、要求はステータス\_バッファー\_の状態を\_小さすぎます。 その後、この要求では、return status ブロックを使用して、pin でサポートされている[**Ksk オーディオ\_\_MIC 配列\_の GEOMETRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)構造体のサイズを示します。

<a name="remarks"></a>解説
-------

\_Ksk プロパティの AUDIO\_MIC\_配列\_ジオメトリプロパティは、ksk プロパティ\_型\_の GET 要求のみをサポートしています。 クライアントが geometry 構造全体を格納するために必要なバッファーの正しいサイズを判断するためには、最初に要求のバッファーサイズをゼロに設定する必要があります。 クライアントは、status ブロックで返された値を使用してバッファーサイズを正しく設定した後、適切なサイズのバッファーで別のプロパティ要求を行うことができます。

Windows でマイクアレイを処理する方法の詳細については、次のリソースを参照してください。

[マイク配列ジオメトリのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/microphone-array-geometry-property)

[Windows でのマイク配列のサポート (ホワイトペーパー)](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613960(v=vs.85))

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIO\_MIC\_配列\_ジオメトリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)

[**KSP\_の PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






