---
title: KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT
description: KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT プロパティが一致を結果のデータを保持します。
ms.assetid: A4CDE539-3C99-4E66-B678-AF56BFFEE460
keywords:
- KSPROPERTY_SOUNDDETECTOR_MATCHRESULT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_MATCHRESULT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a617564ad5c9a50d78e1581dd6c6107403239ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332639"
---
# <a name="kspropertysounddetectormatchresult"></a>KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT


**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**プロパティが一致を結果のデータを保持します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn957513" data-raw-source="[&lt;strong&gt;SOUNDDETECTOR_PATTERNHEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn957513)"><strong>SOUNDDETECTOR_PATTERNHEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A [ **SOUNDDETECTOR\_PATTERNHEADER** ](https://msdn.microsoft.com/library/windows/hardware/dn957513)構造の結果のデータ ペイロードが続きます。

<a name="remarks"></a>注釈
-------

結果のデータが含まれています、 [ **SOUNDDETECTOR\_PATTERNHEADER** ](https://msdn.microsoft.com/library/windows/hardware/dn957513)結果データを処理する OEMDLLCOM オブジェクトと同様に、結果データの形式を指定します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**SOUNDDETECTOR\_PATTERNHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn957513)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






