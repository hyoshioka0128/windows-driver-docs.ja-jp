---
title: KSPROPERTY\_オーディオ\_CPU\_リソース
description: KSPROPERTY\_オーディオ\_CPU\_リソース プロパティは、ノードの機能がハードウェアでの実装や、ホストの CPU で実行されているソフトウェアがエミュレートされるかどうかを指定します。
ms.assetid: 4379aa05-9661-44cd-8f10-0fb37009a4f3
keywords:
- KSPROPERTY_AUDIO_CPU_RESOURCES オーディオ デバイス
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
ms.openlocfilehash: b549a6bc2e32ab23fd3b999450b09e948c22fe39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551496"
---
# <a name="kspropertyaudiocpuresources"></a>KSPROPERTY\_オーディオ\_CPU\_リソース


KSPROPERTY\_オーディオ\_CPU\_リソース プロパティは、ノードの機能がハードウェアでの実装や、ホストの CPU で実行されているソフトウェアがエミュレートされるかどうかを指定します。

## <span id="ddk_ksproperty_audio_cpu_resources_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CPU_RESOURCES_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、ハードウェアまたはソフトウェアで、ノードの機能が実装されているかどうかを示します。 ミニポート ドライバーは、ヘッダー ファイル Ksmedia.h から次の 2 つの定数のいずれかにこの値を設定します。

<span id="KSAUDIO_CPU_RESOURCES_HOST_CPU"></span><span id="ksaudio_cpu_resources_host_cpu"></span>KSAUDIO\_CPU\_リソース\_ホスト\_CPU  
このノードは、ホストの CPU で実行されているソフトウェアの機能を実装します。

<span id="KSAUDIO_CPU_RESOURCES_NOT_HOST_CPU"></span><span id="ksaudio_cpu_resources_not_host_cpu"></span>KSAUDIO\_CPU\_RESOURCES\_NOT\_HOST\_CPU  
このノードは、ハードウェアの機能を実装します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_CPU\_リソース プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、ハードウェアまたはソフトウェアで次のノード型を実装するかどうかを確認するのに使用されます。

-   AEC ノード ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md))

-   ノイズの抑制ノード ([**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md))

-   Peakmeter ノード ([**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md))

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ノイズ\_を抑制します。**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






