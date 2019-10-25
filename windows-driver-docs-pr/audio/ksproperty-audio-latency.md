---
title: KSK プロパティ\_オーディオ\_待機時間
description: KSK プロパティ\_AUDIO\_LATENCY プロパティは、ストリームに関連付けられている遅延 (またはオーディオバッファリングの量) を報告するために使用されます。
ms.assetid: d155e3a5-e3e6-4381-9bbe-2a16b0be47b3
keywords:
- KSPROPERTY_AUDIO_LATENCY オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LATENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7657fc24ebd8a12afc2046c62d5ff7806f787e78
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833020"
---
# <a name="ksproperty_audio_latency"></a>KSK プロパティ\_オーディオ\_待機時間


KSK プロパティ\_AUDIO\_LATENCY プロパティは、ストリームに関連付けられている遅延 (またはオーディオバッファリングの量) を報告するために使用されます。

## <span id="ddk_ksproperty_audio_latency_ks"></span><span id="DDK_KSPROPERTY_AUDIO_LATENCY_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ストリームの待機時間を指定する KSTIME 型の構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_LATENCY プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、AEC フィルターのピンのストリーム待機時間をクエリするために使用されます。 詳細については、「[ハードウェアアクセラレータによるキャプチャ効果の公開](https://docs.microsoft.com/windows-hardware/drivers/audio/exposing-hardware-accelerated-capture-effects)」を参照してください。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSTIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)

 

 






