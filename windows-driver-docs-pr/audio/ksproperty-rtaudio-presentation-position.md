---
title: KSK プロパティ\_RTAUDIO\_プレゼンテーション\_位置
description: KSK プロパティ\_RTAUDIO\_PRESENTATION\_POSITION はストリームプレゼンテーション情報を返します。
ms.assetid: 333A7432-B78A-4F61-B70D-D4F651F90AF7
keywords:
- KSPROPERTY_RTAUDIO_PRESENTATION_POSITION オーディオデバイス
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
ms.openlocfilehash: 68d72d403e3b01996c2c5f91cd7884b8db7b3581
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830602"
---
# <a name="ksproperty_rtaudio_presentation_position"></a>KSK プロパティ\_RTAUDIO\_プレゼンテーション\_位置


KSK プロパティ\_RTAUDIO\_PRESENTATION\_POSITION はストリームプレゼンテーション情報を返します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position"><STRONG>KSAUDIO_PRESENTATION_POSITION</STRONG></a></p></td>
</tr>
</tbody>
</table>
 

プロパティ記述子 (インスタンスデータ) は、 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体です。 クライアントは、要求を送信する前に、オーディオデータストリーム内の現在のカーソル位置を記述する値を使用して構造体を読み込みます。

プロパティ値は、オーディオデータストリーム内の最近のプレゼンテーション位置を表す、 [**ksaudio\_presentation\_position**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position)構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_PRESENTATION\_POSITION プロパティ要求\_は、正常に完了したことを示す状態\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

OS は、上位層がビデオやその他のアクティビティをオーディオストリームと同期できるようにするために、ドライバーから最新のプレゼンテーション位置情報を取得するために、ドライバーからこのプロパティを定期的に取得することができます。

[**Ksaudio\_PRESENTATION\_POSITION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_presentation_position)の u64PositionInBlocks メンバーに返される値は、ksaudio\_rtaudio\_packetcount によって返されるパケット数と同じである必要があります。また、ドライバーの解釈SetWritePacket に渡されるパケット番号。 つまり、パケット0の最初のサンプルはブロック0です。

これは、KSK プロパティ\_RTAUDIO\_PACKETCOUNT と KSK プロパティ\_RTAUDIO\_プレゼンテーション\_位置に同時に呼び出された場合、同じサンプルを参照する値を返すという意味ではありません。 KSK プロパティ\_RTAUDIO\_PACKETCOUNT は、Walastbuffer からハードウェアに転送されたサンプルに関する情報を返しますが、KSK プロパティ\_RTAUDIO\_PRESENTATION\_POSITION はサンプルに関する情報を返しますシステムの出力に表示されます。 これらは2つの異なる情報です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

 

 






