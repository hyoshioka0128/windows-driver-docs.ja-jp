---
title: KSK プロパティ\_テレフォニー\_CALLCONTROL
description: スマートフォンの開始と終了には、KSK プロパティ\_テレフォニー\_CALLCONTROL プロパティが使用されます。
ms.assetid: AAC2A218-9A2D-4EFE-B609-5078028B2426
keywords:
- KSPROPERTY_TELEPHONY_CALLCONTROL オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLCONTROL
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d8543f4400854cfd9e3fc59e2609d555d183a7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830477"
---
# <a name="ksproperty_telephony_callcontrol"></a>KSK プロパティ\_テレフォニー\_CALLCONTROL


スマートフォンの開始と終了には、KSK プロパティ\_テレフォニー\_CALLCONTROL プロパティが使用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLCONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol)"><strong>KSTELEPHONY_CALLCONTROL</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

TELEPHONY プロパティ\_TELEPHONY\_CALLCONTROL プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_テレフォニー\_CALLCONTROL には、CallType および Callcontrol Lop に関する情報が含まれています。

テレフォニー\_呼び出し制御 LOP\_有効にすると、オーディオドライバーの観点から携帯電話の通話が開始され、関連付けられている携帯電話の bidi エンドポイントのジャックの状態がアクティブに更新され、呼び出しの種類が保存され、呼び出しの状態が [有効] に更新されます。

テレフォニー\_呼び出し制御 LOP\_DISABLE は、オーディオドライバーの観点からの携帯電話通話を終了し、関連付けられている携帯電話の bidi エンドポイントのジャックの状態を "切断" に更新して、呼び出しの状態を "無効" に更新します。 この場合、呼び出しの種類は無視されます。

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
<td align="left"><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





