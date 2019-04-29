---
title: KSPROPERTY\_TOPOLOGYNODE\_を有効にします。
description: KSPROPERTY\_TOPOLOGYNODE\_有効にするプロパティをオンまたはオフ、既にビルドされたトポロジでのトポロジのノードに使用します。
ms.assetid: 6b9f7a92-97dc-476b-962a-40ccf1987154
keywords:
- KSPROPERTY_TOPOLOGYNODE_ENABLE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a59b13d9b73b7d7566b29df7adfc4e1dd88305
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332556"
---
# <a name="kspropertytopologynodeenable"></a>KSPROPERTY\_TOPOLOGYNODE\_を有効にします。


KSPROPERTY\_TOPOLOGYNODE\_有効にするプロパティをオンまたはオフ、既にビルドされたトポロジでのトポロジのノードに使用します。

## <span id="ddk_ksproperty_topologynode_enable_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_ENABLE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は BOOL 型のノードがオンまたはオフになっているかどうかを指定します。 値**TRUE**ノードが有効であることを示します。 **FALSE**ノードが無効になっていることを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_TOPOLOGYNODE\_有効にするプロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

既に有効になっているノードの有効化または、既に無効になっているノードを無効にする、影響を与えませんが、エラーとして扱うことはできません。

ノードを無効にすると、ノードを通過するストリームをノードを実行する変換オフにします。 場合は、AEC、AGC、またはノイズ抑制ノード ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)、 [ **KSNODETYPE\_AGC**](ksnodetype-agc.md)、または[ **KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md))、たとえば、無効になっているノードの動作パススルー モード (つまり、演算を実行しないストリームでノードの入力ピンから、出力ピンに流れる)。

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

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_ノイズ\_を抑制します。**](ksnodetype-noise-suppress.md)

 

 






