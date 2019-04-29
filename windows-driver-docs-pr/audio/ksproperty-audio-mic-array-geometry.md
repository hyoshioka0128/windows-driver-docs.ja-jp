---
title: KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY
description: KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY プロパティがマイク配列のジオメトリを指定します。
ms.assetid: c9153c65-06d1-4968-8d70-64aafc760a8c
keywords:
- KSPROPERTY_AUDIO_MIC_ARRAY_GEOMETRY オーディオ デバイス
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
ms.openlocfilehash: 129d60dc933d6053dad78ebfab2507af408e0edb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333030"
---
# <a name="kspropertyaudiomicarraygeometry"></a>KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY


KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY プロパティがマイク配列のジオメトリを指定します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537087" data-raw-source="[&lt;strong&gt;KSAUDIO_MIC_ARRAY_GEOMETRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537087)"><strong>KSAUDIO_MIC_ARRAY_GEOMETRY</strong></a></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) が型 KSAUDIO\_MIC\_配列\_ジオメトリ。 定義を参照してください、 [ **KSAUDIO\_MIC\_配列\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537087)詳細については、構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY プロパティ要求がステータスを返す\_要求が正常に完了すると成功します。

PinId メンバーによって、暗証番号 (pin) が示される場合、 [ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)構造体は、mic の配列の要求をサポートしていません、プロパティの要求が状態を返す\_いない\_サポートされています。

プロパティ要求が状態を返す要求のバッファー サイズがゼロに設定されている場合\_バッファー\_オーバーフロー状態。 さらに、要求がブロックを使用して、状態の戻り値、KSAUDIO のサイズを示す\_MIC\_配列\_暗証番号 (pin) でサポートされている GEOMETRY 構造体。

要求のバッファー サイズが小さすぎて返された構造体に対応するバッファーのサイズに設定されている場合、要求がのステータスを返します\_バッファー\_すぎます\_小さい。 要求のサイズを示すために状態の戻り値のブロックを使用して、 [ **KSAUDIO\_MIC\_配列\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537087)暗証番号 (pin) でサポートされている構造体。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_オーディオ\_MIC\_配列\_GEOMETRY プロパティは、KSPROPERTY のみがサポートされます。\_型\_GET 要求。 クライアントは、ジオメトリ全体の構造を対応するために必要なバッファーの適切なサイズを調べるためには、最初に、バッファー サイズが 0 の要求を作成する必要があります。 クライアントは、バッファー サイズを正しく設定する状態のブロックで返される値を使用し、正しいサイズのバッファーで別のプロパティの要求を加えます。

Windows でのマイク配列を処理する方法の詳細については、次の情報を参照してください。

[Windows (ホワイト ペーパー) でのマイク配列のサポート](https://go.microsoft.com/fwlink/p/?linkid=120592)

[マイク配列 Geometry プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff537516.aspx)

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


[**KSAUDIO\_MIC\_配列\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)

[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

 

 






