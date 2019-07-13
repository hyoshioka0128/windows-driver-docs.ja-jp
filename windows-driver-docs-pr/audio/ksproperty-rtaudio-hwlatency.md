---
title: KSPROPERTY\_RTAUDIO\_HWLATENCY
description: KSPROPERTY\_RTAUDIO\_HWLATENCY プロパティは、オーディオ ハードウェアとの関連付けられているデータ パスのストリームの待機時間の記述を取得します。 次の表では、このプロパティの機能をまとめたものです。
ms.assetid: 5083f281-853a-464e-95d3-0fe14fe00c1c
keywords:
- KSPROPERTY_RTAUDIO_HWLATENCY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_HWLATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1d3d49100d15c584c419b7d42d821ed3da516501
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866477"
---
# <a name="kspropertyrtaudiohwlatency"></a>KSPROPERTY\_RTAUDIO\_HWLATENCY


KSPROPERTY\_RTAUDIO\_HWLATENCY プロパティは、オーディオ ハードウェアとの関連付けられているデータ パスのストリームの待機時間の記述を取得します。

次の表では、このプロパティの機能をまとめたものです。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwlatency"><strong>KSRTAUDIO_HWLATENCY</strong></a></p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_HWLATENCY プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

後に、 [WaveRT ミニポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)循環バッファーの割り当てが (を参照してください[ **KSPROPERTY\_RTAUDIO\_バッファー**](ksproperty-rtaudio-buffer.md))、クライアントが送信できる、KSPROPERTY\_RTAUDIO\_HWLATENCY プロパティ ドライバー ハードウェア待機時間情報を要求します。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_HWLATENCY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwlatency)

[**KSPROPERTY\_RTAUDIO\_バッファー**](ksproperty-rtaudio-buffer.md)

[**WaveRT ミニポート ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)
