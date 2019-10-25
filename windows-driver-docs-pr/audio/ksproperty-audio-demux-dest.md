---
title: KSK プロパティ\_AUDIO\_DEMUX\_DEST
description: KSK プロパティ\_AUDIO\_DEMUX\_DEST プロパティは、デマルチプレクサーが入力ストリームを送信する宛先ストリームを指定します。 これは、DEMUX ノード (KSNODETYPE\_DEMUX) のプロパティです。
ms.assetid: 431918da-2267-4fe5-a002-12d16b5f0984
keywords:
- KSPROPERTY_AUDIO_DEMUX_DEST オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DEMUX_DEST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 556475d73c36544074687e1ebf38459bd0efb5a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831045"
---
# <a name="ksproperty_audio_demux_dest"></a>KSK プロパティ\_AUDIO\_DEMUX\_DEST


KSK プロパティ\_AUDIO\_DEMUX\_DEST プロパティは、デマルチプレクサーが入力ストリームを送信する宛先ストリームを指定します。 これは、DEMUX ノード ([**KSNODETYPE\_demux**](ksnodetype-demux.md)) のプロパティです。

## <span id="ddk_ksproperty_audio_demux_dest_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DEMUX_DEST_KS"></span>


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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG です。 この値は、DEMUX ノード上の選択された出力ピンの pin ID です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_DEMUX\_DEST property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

Pin ID は、DEMUX ノードの論理ピンを識別します。 フィルター内のノードの論理ピンの pin Id の詳細については、「 [**Pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))」を参照してください。

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


[**KSNODETYPE\_DEMUX**](ksnodetype-demux.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))

 

 






