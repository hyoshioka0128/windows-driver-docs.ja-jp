---
title: KSPROPERTY\_AC3\_ミックス ダウン
description: KSPROPERTY\_AC3\_ミックス ダウン プロパティは、AC で 3 でエンコードされたストリームでプログラムのチャネルがスピーカーの構成に合わせてミックス ダウンをする必要があるかどうかを指定します。
ms.assetid: 1d47f890-f7da-423f-adef-72b06a0f79d8
keywords:
- KSPROPERTY_AC3_DOWNMIX オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_DOWNMIX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba14a887b9992fd7f1d60467b3652f283f4092b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560532"
---
# <a name="kspropertyac3downmix"></a>KSPROPERTY\_AC3\_ミックス ダウン


KSPROPERTY\_AC3\_ミックス ダウン プロパティは、AC で 3 でエンコードされたストリームでプログラムのチャネルがスピーカーの構成に合わせてミックス ダウンをする必要があるかどうかを指定します。

## <span id="ddk_ksproperty_ac3_downmix_ks"></span><span id="DDK_KSPROPERTY_AC3_DOWNMIX_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537079" data-raw-source="[&lt;strong&gt;KSAC3_DOWNMIX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537079)"><strong>KSAC3_DOWNMIX</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSAC3\_ミックス ダウン構造プログラム チャネルがミックス ダウンをするかどうかを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_ミックス ダウン プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

デコーダーによって出力されるチャネルの数が、ac-3 ストリームにエンコードするチャネルの数より小さい場合、ミックス ダウンする必要があります。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAC3\_ミックス ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff537079)

 

 






