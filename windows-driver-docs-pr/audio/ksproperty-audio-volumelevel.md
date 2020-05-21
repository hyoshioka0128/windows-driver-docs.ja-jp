---
title: KSK プロパティ \_ AUDIO \_ VOLUMELEVEL
description: KSK PROPERTY \_ AUDIO \_ VOLUMELEVEL プロパティは、ボリュームノード (KSNODETYPE ボリューム) 内のチャネルのボリュームレベルを指定し \_ ます。
ms.assetid: 5b420c71-fc82-413d-a93d-e8f3408cc8d7
keywords:
- KSPROPERTY_AUDIO_VOLUMELEVEL オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19771178e6302931490019fb2dd39ee6ac3a8085
ms.sourcegitcommit: 7ee048ef0b2928b5fd372d6fe5d6c0c008462180
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83729552"
---
# <a name="ksproperty_audio_volumelevel"></a>KSK プロパティ \_ AUDIO \_ VOLUMELEVEL


KSK PROPERTY \_ AUDIO \_ VOLUMELEVEL プロパティは、ボリュームノード ([**KSNODETYPE \_ ボリューム**](ksnodetype-volume.md)) 内のチャネルのボリュームレベルを指定します。

## <span id="ddk_ksproperty_audio_volumelevel_ks"></span><span id="DDK_KSPROPERTY_AUDIO_VOLUMELEVEL_KS"></span>


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
<th align="left">取得</th>
<th align="left">オン</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルターまたは Pin インスタンスを使用したノード</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値は LONG 型で、指定されたストリームのチャネルのボリュームレベルを指定します。 ボリュームレベルの値には、次のスケールが使用されます。

-2147483648 は-無限大デシベル (減衰),

-2147483647 は-32767.99998474 デシベル (減衰)、および

+ 2147483647 は + 32767.99998474 デシベル (ゲイン) です。

> [!Note]
> デシベル範囲は、-2147483648 ~ + 2147483647 の整数値によって表されます。このスケールでは、1/65536 デシベルが解決されます。

 

値がフィルターの範囲を超えて指定されている場合でも、このプロパティを設定する要求は成功します。 ただし、フィルターに適用された実際の値は、このプロパティの後続の Get 呼び出しによってのみ決定できます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK PROPERTY \_ AUDIO \_ VOLUMELEVEL property 要求は、 \_ 正常に完了したことを示すステータス成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>解説
-------

このプロパティのプロパティ記述子は、チャネル番号を指定します。 ボリュームノードを通過するストリームに*n 個*のチャネルが含まれている場合、チャネルには 0 ~ *n*-1 の番号が付けられます。 詳細については、「[マルチチャネルノードの公開](https://docs.microsoft.com/windows-hardware/drivers/audio/exposing-multichannel-nodes)」を参照してください。

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


[既定のオーディオボリューム設定のカスタマイズ](https://docs.microsoft.com/windows-hardware/drivers/audio/customizing-default-audio-volume-settings)

[既定のオーディオ音量の設定](https://docs.microsoft.com/windows-hardware/drivers/audio/default-audio-volume-settings)

[**KSNODEPROPERTY \_ オーディオ \_ チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE \_ ボリューム**](ksnodetype-volume.md)

 

 






