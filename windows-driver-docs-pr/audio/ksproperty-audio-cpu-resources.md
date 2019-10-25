---
title: KSK プロパティ\_AUDIO\_CPU\_リソース
description: KSK プロパティ\_AUDIO\_CPU\_RESOURCES プロパティは、ノードの機能をハードウェアに実装するか、ホストの CPU で実行されるソフトウェアでエミュレートするかを指定します。
ms.assetid: 4379aa05-9661-44cd-8f10-0fb37009a4f3
keywords:
- KSPROPERTY_AUDIO_CPU_RESOURCES オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CPU_RESOURCES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 286e988e4bf16c20b016cba464270a9b4c10e500
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831052"
---
# <a name="ksproperty_audio_cpu_resources"></a>KSK プロパティ\_AUDIO\_CPU\_リソース


KSK プロパティ\_AUDIO\_CPU\_RESOURCES プロパティは、ノードの機能をハードウェアに実装するか、ホストの CPU で実行されるソフトウェアでエミュレートするかを指定します。

## <span id="ddk_ksproperty_audio_cpu_resources_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CPU_RESOURCES_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG で、ノードの機能がハードウェアまたはソフトウェアに実装されているかどうかを示します。 ミニポートドライバーは、ヘッダーファイル Ksmedia. h から、次の2つの定数のいずれかにこの値を設定します。

<span id="KSAUDIO_CPU_RESOURCES_HOST_CPU"></span><span id="ksaudio_cpu_resources_host_cpu"></span>KSAUDIO\_CPU\_リソース\_ホスト\_CPU  
このノードは、ホストの CPU で実行されるソフトウェアにその機能を実装します。

<span id="KSAUDIO_CPU_RESOURCES_NOT_HOST_CPU"></span><span id="ksaudio_cpu_resources_not_host_cpu"></span>KSAUDIO\_CPU\_リソース\_\_ホスト\_CPU  
このノードは、ハードウェアでその機能を実装します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_CPU\_RESOURCES プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、ハードウェアまたはソフトウェアに次のノードの種類が実装されているかどうかを判断するために使用されます。

-   AEC ノード ([**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md))

-   ノイズ抑制ノード ([**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md))

-   Peakmeter ノード ([**KSNODETYPE\_peakmeter**](ksnodetype-peakmeter.md))

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






