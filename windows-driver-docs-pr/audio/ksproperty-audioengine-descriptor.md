---
title: KSPROPERTY\_AUDIOENGINE\_記述子
description: オフロード機能を備えたハードウェア ソリューションのオーディオ ドライバーの使用 KSPROPERTY\_AUDIOENGINE\_記述子をハードウェアのオーディオ エンジンを表すノードに関する情報を提供します。
ms.assetid: 1D912155-6DB2-4AFF-949F-47C19E47678C
keywords:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 090b206274bad3d6693b5b753163773d6b91db60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332872"
---
# <a name="kspropertyaudioenginedescriptor"></a>KSPROPERTY\_AUDIOENGINE\_記述子


オフロード機能を備えたハードウェア ソリューションのオーディオ ドライバーを使用して**KSPROPERTY\_AUDIOENGINE\_記述子**ハードウェア オーディオ エンジンを表すノードに関する情報を提供します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450862" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450862)"><strong>KSAUDIOENGINE_DESCRIPTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型**KSAUDIOENGINE\_記述子**オーディオ エンジン ノードの静的プロパティを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOENGINE\_記述子**プロパティ要求を返します**状態\_成功**を正常に完了したことを示します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="requirements"></a>必要条件
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


[**KSAUDIOENGINE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/hh450862)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






