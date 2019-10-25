---
title: KSK プロパティ\_AUDIO\_POSITIONEX
description: KSK プロパティ\_AUDIO\_POSITIONEX プロパティは、ストリームの位置と、カーネルストリーミング (KS) ベースのオーディオドライバーに関連付けられたタイムスタンプ情報を呼び出し元に提供します。
ms.assetid: 660b1ee9-7c52-4d95-8df9-b1c0dce320e3
keywords:
- KSPROPERTY_AUDIO_POSITIONEX オーディオデバイス
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
ms.openlocfilehash: e17680a0e114e77e111aac06814a4a0517d8ac03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832943"
---
# <a name="ksproperty_audio_positionex"></a>KSK プロパティ\_AUDIO\_POSITIONEX


KSK プロパティ\_AUDIO\_POSITIONEX プロパティは、ストリームの位置と、カーネルストリーミング (KS) ベースのオーディオドライバーに関連付けられたタイムスタンプ情報を呼び出し元に提供します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex" data-raw-source="[&lt;strong&gt;KSAUDIO_POSITIONEX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)"><strong>KSAUDIO_POSITIONEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、プロパティハンドラーから位置情報を受け取る KSK AUDIO\_POSITIONEX 型の構造体です。 KSAUDIO\_POSITIONEX 構造体によって指定された位置情報は、呼び出し元によって選択されたピンの位置情報です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_POSITIONEX プロパティ要求では、呼び出しが成功した場合には\_OK が返されます。 それ以外の場合は、適切な HRESULT エラーコードを返します。

<a name="remarks"></a>注釈
-------

通常、オーディオアプリケーションでは、オーディオストリームの現在位置を監視する必要があります。 この位置は、ストリームの先頭からのバイトオフセットとして指定されます。 ストリームの位置情報には、次の2つの解釈が考えられます。

-   レンダリングストリームの場合、ストリームの位置は、デジタル-アナログコンバーター (Dac) を通じて現在再生されているオーディオフレームのバイトオフセットです。

-   キャプチャストリームの場合、ストリームの位置は、現在アナログ-デジタルコンバーター (ADCs) を介して記録されているオーディオフレームのバイトオフセットです。

KSK プロパティ\_AUDIO\_POSITIONEX プロパティをサポートするドライバーは、ストリームの位置の値に対してタイムスタンプウィンドウを生成します。 タイムスタンプウィンドウは、ストリームの位置を決定する前にサンプリングされるタイムスタンプと、ストリームの位置が決定された後に取得されるタイムスタンプの間の間隔です。 次に、呼び出し元は、タイムスタンプウィンドウを使用できるかどうかを判断します。

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
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIO\_POSITIONEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_positionex)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






