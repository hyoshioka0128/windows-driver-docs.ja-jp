---
title: KSPROPERTY\_AUDIOENGINE\_MIXFORMAT
description: KSPROPERTY\_AUDIOENGINE\_MIXFORMAT プロパティ要求が、ハードウェアのオーディオ エンジンでミキサーの設定を取得します。
ms.assetid: 12353E72-1092-44B4-861A-90C198237670
keywords:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b37f79839e0fef2f95e0b48bfc758ba6d946abb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551297"
---
# <a name="kspropertyaudioenginemixformat"></a>KSPROPERTY\_AUDIOENGINE\_MIXFORMAT


**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**プロパティ要求が、ハードウェアのオーディオ エンジンでミキサーの設定を取得します。

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
<td align="left"><p>フィルターを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537095" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537095)"><strong>KSDATAFORMAT_WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**プロパティ要求を返します**状態\_成功**を正常に完了したことを示します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

ミックス形式のオーディオ エンジン ノードで任意の時点で設定されているは、オフロード pin ファクトリによってもサポートする必要があります。

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






