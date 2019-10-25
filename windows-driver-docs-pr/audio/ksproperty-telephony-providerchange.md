---
title: KSK プロパティ\_テレフォニー\_PROVIDERCHANGE
description: KSK プロパティ\_TELEPHONY\_PROVIDERCHANGE プロパティは、シングルラジオ音声通話の継続性 (SRVCC) が開始または終了するオーディオドライバーとの通信に使用されます。
ms.assetid: 9CEDAFE7-014F-4670-958D-6D3687D2D24A
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERCHANGE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_PROVIDERCHANGE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c0f6c69d1c9573c5a049be517db988d03dc5ff4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832687"
---
# <a name="ksproperty_telephony_providerchange"></a>KSK プロパティ\_テレフォニー\_PROVIDERCHANGE


**Ksk プロパティ\_TELEPHONY\_PROVIDERCHANGE**プロパティは、シングルラジオ音声通話の継続性 (srvcc) が開始または終了するオーディオドライバーとの通信に使用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange" data-raw-source="[&lt;strong&gt;KSTELEPHONY_PROVIDERCHANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)"><strong>KSTELEPHONY_PROVIDERCHANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は[**KSTELEPHONY\_providerchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)で、電話の種類とプロバイダーの変更操作の種類を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_TELEPHONY\_PROVIDERCHANGE** property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

オーディオスタックは、 [**KSTELEPHONY\_PROVIDERCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstelephony_providerchange)プロパティを使用して、オーディオドライバーへの srvcc の開始と終了を示します。 このプロパティは、呼び出しの種類 (LTE パケットスイッチ、WLAN パケット切り替え、またはサーキットスイッチ) とプロバイダー変更操作 (開始、終了、またはキャンセル) をドライバーに伝達します。 プロバイダー操作が SRVCC を終了するために使用されている場合、呼び出しの種類は無視されます。

プロバイダーの変更操作が**テレフォニー\_PROVIDERCHANGEOP\_開始**されると、ドライバーはそのプロバイダーの呼び出し状態を**テレフォニー\_CALLSTATE\_providertransition**に更新します。 プロバイダーの変更操作が**テレフォニー\_PROVIDERCHANGEOP\_終了**すると、ドライバーはそのプロバイダーの呼び出し状態を**テレフォニー\_CALLSTATE\_有効**に更新します。 SRVCC では、ドライバーは、関連付けられている[**KSNODETYPE\_テレフォニー\_BIDI**](ksnodetype-telephony-bidi.md)エンドポイントを引き続き使用する必要があり、このエンドポイントのジャックの状態は変更しません。 プロバイダーの変更操作がテレフォニーの場合 **\_PROVIDERCHANGEOP\_キャンセル**, srvcc はキャンセルされ、ドライバーは srvcc 呼び出しの前に戻ります。

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

 

 





