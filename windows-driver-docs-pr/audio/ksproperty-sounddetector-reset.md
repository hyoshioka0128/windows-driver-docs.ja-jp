---
title: KSK プロパティ\_SOUNDDETECTOR\_リセット
description: '\_SOUNDDETECTOR\_RESET プロパティは、パターンが設定されていない unarmed 状態に検出をリセットします。'
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664D
keywords:
- KSPROPERTY_SOUNDDETECTOR_RESET オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_RESET
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2890f4d2d12fc44c17f3dc1991af486af0d3d328
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830577"
---
# <a name="ksproperty_sounddetector_reset"></a>KSK プロパティ\_SOUNDDETECTOR\_リセット

**\_SOUNDDETECTOR\_RESET**プロパティは、パターンが設定されていない unarmed 状態に検出をリセットします。

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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値はブール値です。 True はリセットすることを示し、false は無視されます。

<a name="remarks"></a>注釈
-------

OS は、次のような場合に true の値を設定して reset を呼び出します。

- キーワード検出機能をアン arm します。
- 設定されているパターン\_、すべての[**Ksproperty\_SOUNDDETECTOR**](ksproperty-sounddetector-patterns.md)をクリアします。

キーワードパターンが設定されていないときにこの true を設定した場合 ([**Ksk プロパティ\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)が空の場合)、効果はありません。

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
<td align="left"><p>Windows 10 バージョン1903</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[**KSK プロパティ\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

[**KSSOUNDDETECTORPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/)
