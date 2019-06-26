---
title: KSPROPERTY\_オーディオ\_POSITIONEX
description: KSPROPERTY\_オーディオ\_POSITIONEX プロパティは、ストリームの位置と関連付けられているタイムスタンプ情報をストリーミング (KS) カーネルの呼び出し元のオーディオ ドライバーのベースします。
ms.assetid: 660b1ee9-7c52-4d95-8df9-b1c0dce320e3
keywords:
- KSPROPERTY_AUDIO_POSITIONEX オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_POSITIONEX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5f6c03e63c0dc6699d3826d315f03d55ee25b3b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391469"
---
# <a name="kspropertyaudiopositionex"></a>KSPROPERTY\_オーディオ\_POSITIONEX


KSPROPERTY\_オーディオ\_POSITIONEX プロパティは、ストリームの位置と関連付けられているタイムスタンプ情報をストリーミング (KS) カーネルの呼び出し元のオーディオ ドライバーのベースします。

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
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_positionex" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITIONEX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_positionex)"><strong>KSAUDIO_POSITIONEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_POSITIONEX プロパティ ハンドラーから位置情報を受け取る。 位置情報、KSAUDIO で指定されている\_POSITIONEX 構造は、呼び出し元によって選択された暗証番号 (pin) の位置情報。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_POSITIONEX プロパティ要求を返します。 S\_了解の呼び出しが成功した場合。 それ以外の場合、適切な HRESULT エラー コードを返します。

<a name="remarks"></a>注釈
-------

通常、オーディオのアプリケーションは、オーディオ ストリームの現在の位置を監視する必要があります。 この位置はストリームの先頭からのバイト オフセットとして指定されます。 これには、ストリームの位置情報の 2 つの可能な解釈があります。

-   レンダリング ストリームの場合は、ストリームの位置は、アナログ デジタル コンバーター (Dac) を使って現在再生されているオーディオ フレームのバイト オフセットは。

-   キャプチャ ストリームの場合、ストリームの位置は、アナログ/デジタル コンバーター (Adc) を使って現在記録中のオーディオのフレームのバイト オフセットです。

KSPROPERTY をサポートしているドライバー\_オーディオ\_POSITIONEX プロパティには、ストリームの位置の値のタイムスタンプ ウィンドウが生成されます。 タイムスタンプのウィンドウは、ストリームの位置を決定する前にサンプリングされるタイムスタンプとは、ストリームの位置を決定したら、取得したタイムスタンプの間の間隔です。 呼び出し元では、タイムスタンプのウィンドウを使用できるかどうかを決定します。

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
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSAUDIO\_POSITIONEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






