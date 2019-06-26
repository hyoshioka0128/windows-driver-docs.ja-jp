---
title: KSPROPERTY\_AEC\_ノイズ\_入力\_を有効にします。
description: KSPROPERTY\_AEC\_ノイズ\_入力\_を有効にして、バック グラウンド ノイズの塗りつぶしを無効化を有効にするプロパティを使用します。 これは省略可能な AEC ノードのプロパティ (KSNODETYPE\_音響\_エコー\_キャンセル)。
ms.assetid: 7c0ed4ba-d25e-42b5-b213-fbe74040a453
keywords:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3471bc3b5f8e03dd245a9a742b6b59c2f401487
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358973"
---
# <a name="kspropertyaecnoisefillenable"></a>KSPROPERTY\_AEC\_ノイズ\_入力\_を有効にします。


KSPROPERTY\_AEC\_ノイズ\_入力\_を有効にして、バック グラウンド ノイズの塗りつぶしを無効化を有効にするプロパティを使用します。 これは省略可能な AEC ノードのプロパティ ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_noise_fill_enable_ks"></span><span id="DDK_KSPROPERTY_AEC_NOISE_FILL_ENABLE_KS"></span>


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
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、BOOL 型のです。 この値を設定**TRUE**バック グラウンド ノイズいっぱいになるようにします。 有効にすると、ノードはバック グラウンド ノイズをキャプチャ ストリームに挿入します。 この値を設定**FALSE**バック グラウンド ノイズの塗りつぶしを無効にします。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AEC\_ノイズ\_入力\_有効にするプロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

AEC のノードは、キャプチャされたデータ ストリームが完璧なエコー キャンセル後に 0 に設定されているときに発生する不自然無音状態を回避するために、キャプチャ ストリームに雑音快適性を挿入します。

AEC ノードを含んでいるフィルターが作成されるか、ノードがリセットされた、バック グラウンド ノイズを埋めるは既定で無効になっています。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

 

 






