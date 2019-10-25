---
title: KSK プロパティ\_RTAUDIO\_HWLATENCY
description: KSK プロパティ\_RTAUDIO\_HWLATENCY プロパティは、オーディオハードウェアのストリーム待機時間とそれに関連付けられているデータパスの説明を取得します。 次の表は、このプロパティの機能をまとめたものです。
ms.assetid: 5083f281-853a-464e-95d3-0fe14fe00c1c
keywords:
- KSPROPERTY_RTAUDIO_HWLATENCY オーディオデバイス
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
ms.openlocfilehash: 6b6717f37170aa261837734a44b0f43b1338c61a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830681"
---
# <a name="ksproperty_rtaudio_hwlatency"></a>KSK プロパティ\_RTAUDIO\_HWLATENCY


KSK プロパティ\_RTAUDIO\_HWLATENCY プロパティは、オーディオハードウェアのストリーム待機時間とそれに関連付けられているデータパスの説明を取得します。

次の表は、このプロパティの機能をまとめたものです。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwlatency"><strong>KSRTAUDIO_HWLATENCY</strong></a></p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_HWLATENCY property 要求\_は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

[Walastミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)によって循環バッファーが割り当てられた後 (「 [**KSK プロパティ\_rtaudio\_buffer**](ksproperty-rtaudio-buffer.md)」を参照してください)、クライアントは、rtaudio\_HWLATENCY property 要求に対して、ハードウェア待機時間のために ksk\_プロパティをドライバーに送信できます。参照.

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_HWLATENCY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwlatency)

[**KSK プロパティ\_RTAUDIO\_BUFFER**](ksproperty-rtaudio-buffer.md)

[**WaveRT ミニポートドライバー**](https://docs.microsoft.com/windows-hardware/drivers/audio/wavert-miniport-driver)
