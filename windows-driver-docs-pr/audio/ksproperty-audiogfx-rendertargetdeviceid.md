---
title: KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID
description: KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID プロパティは、最終的なオーディオ ミックスをレンダリングするオーディオ デバイスのプラグ アンド プレイ デバイス ID の GFX フィルターを通知するために使用します。
ms.assetid: 66251f22-a2e3-453e-985a-74ff18a60e66
keywords:
- KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 552c112480acb840cccafb8f1d38bfa9baa8187b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391454"
---
# <a name="kspropertyaudiogfxrendertargetdeviceid"></a>KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID


KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID プロパティは、最終的なオーディオ ミックスをレンダリングするオーディオ デバイスのプラグ アンド プレイ デバイス ID の GFX フィルターを通知するために使用します。

## <span id="ddk_ksproperty_audiogfx_rendertargetdeviceid_ks"></span><span id="DDK_KSPROPERTY_AUDIOGFX_RENDERTARGETDEVICEID_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>WCHAR 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、デバイス ID を格納している WCHAR 配列 デバイス ID は、Unicode 文字の null で終わる文字列です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AUDIOGFX\_RENDERTARGETDEVICEID プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティのセットのみ要求のターゲットは、レンダリングのまたは GFX キャプチャ-レンダー/フィルターとして使用するために構成されている GFX フィルターです。

プロパティ値を保持するために必要なバッファーのサイズを確認するのを参照してください。[オーディオのプロパティの基本的なクエリがサポート](https://docs.microsoft.com/windows-hardware/drivers/audio/basic-support-queries-for-audio-properties)します。

デバイス Id の詳細については、次を参照してください。[識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)します。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






