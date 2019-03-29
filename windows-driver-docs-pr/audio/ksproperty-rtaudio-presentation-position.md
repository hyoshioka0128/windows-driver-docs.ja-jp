---
title: KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置
description: KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置がストリームのプレゼンテーションの情報を返します。
ms.assetid: 333A7432-B78A-4F61-B70D-D4F651F90AF7
keywords:
- KSPROPERTY_RTAUDIO_PRESENTATION_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_PRESENTATION_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 01/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: aaa3bc9613bd4e57d3b181015ddee9baeaeb8b3a
ms.sourcegitcommit: 239b10612b3ddb6702dc16490566069cc3aa1c6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2019
ms.locfileid: "56582718"
---
# <a name="kspropertyrtaudiopresentationposition"></a>KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置


KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置がストリームのプレゼンテーションの情報を返します。

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
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_presentation_position"><STRONG>KSAUDIO_PRESENTATION_POSITION</STRONG></a></p></td>
</tr>
</tbody>
</table>
 

プロパティ記述子 (インスタンス データ) が、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 要求を送信する前に、クライアントは、オーディオ データ ストリームの現在のカーソル位置を示す値を持つ構造体を読み込みます。

プロパティの値は、 [ **KSAUDIO\_プレゼンテーション\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450865)オーディオ データ ストリーム内の最近使用したプレゼンテーション位置を表す構造体です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

OS は、オーディオ ストリームとビデオやその他のアクティビティを同期する上位の層を許可するには、ドライバーから最近使用したプレゼンテーションの位置情報を取得するドライバーからこのプロパティを定期的に取得可能性があります。

U64PositionInBlocks メンバーでは、値が返される[ **KSAUDIO\_プレゼンテーション\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450865) KSPROPERTYによって返されるパケットの数と一致する必要があります\_RTAUDIO\_PACKETCOUNT とパケットの数のドライバーの解釈 SetWritePacket に渡されます。 つまり、パケットが 0 の最初のサンプルには、ブロック 0 です。

限りませんその KSPROPERTY\_RTAUDIO\_PACKETCOUNT と KSPROPERTY\_RTAUDIO\_プレゼンテーション\_位置、同時に、呼び出された場合は値を返し、同じサンプルを参照してください。 KSPROPERTY\_RTAUDIO\_PACKETCOUNT が WaveRT バッファーから KSPROPERTY 中に、ハードウェアに転送されるサンプルに関する情報を返します\_RTAUDIO\_プレゼンテーション\_位置を返します。システムの出力を紹介するサンプルについて説明します。 これらは、2 つの異なる情報です。

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
<td align="left"><p>Windows 10 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

 

 






