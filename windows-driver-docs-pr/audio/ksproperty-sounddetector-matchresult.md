---
title: '\_MATCHRESULT の KSK プロパティ\_SOUNDDETECTOR'
description: '\_MATCHRESULT プロパティの KSK プロパティ\_、一致の結果データを保持します。'
ms.assetid: A4CDE539-3C99-4E66-B678-AF56BFFEE460
keywords:
- KSPROPERTY_SOUNDDETECTOR_MATCHRESULT オーディオデバイス
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
ms.openlocfilehash: 9338934114d7e341d98dc0185b38e161b4ccc69d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830586"
---
# <a name="ksproperty_sounddetector_matchresult"></a>\_MATCHRESULT の KSK プロパティ\_SOUNDDETECTOR


**\_MATCHRESULT プロパティの Ksk プロパティ\_** 、一致の結果データを保持します。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader" data-raw-source="[&lt;strong&gt;SOUNDDETECTOR_PATTERNHEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)"><strong>SOUNDDETECTOR_PATTERNHEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

サウンド検出機能によって、 [**PATTERN ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)構造の後に結果データペイロードが\_されます。

<a name="remarks"></a>注釈
-------

結果データには、結果データの形式を識別する[**PATTERN ヘッダー\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader) 、結果データを処理する OEMDLLCOM オブジェクトも含まれます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**SOUNDDETECTOR\_PATTERN ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






