---
title: KSPROPERTY\_テレフォニー\_PROVIDERCHANGE
description: KSPROPERTY\_テレフォニー\_PROVIDERCHANGE プロパティは、単一ラジオ音声通話の継続性 (SRVCC) が開始または終了するオーディオ ドライバーとの通信に使用します。
ms.assetid: 9CEDAFE7-014F-4670-958D-6D3687D2D24A
keywords:
- KSPROPERTY_TELEPHONY_PROVIDERCHANGE オーディオ デバイス
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
ms.openlocfilehash: 0cc68047a87b0babae1d7cf1e80d6c751d527fa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573213"
---
# <a name="kspropertytelephonyproviderchange"></a>KSPROPERTY\_テレフォニー\_PROVIDERCHANGE


**KSPROPERTY\_テレフォニー\_PROVIDERCHANGE**プロパティは、単一ラジオ音声通話の継続性 (SRVCC) が開始または終了するオーディオ ドライバーとの通信に使用します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169885" data-raw-source="[&lt;strong&gt;KSTELEPHONY_PROVIDERCHANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169885)"><strong>KSTELEPHONY_PROVIDERCHANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型[ **KSTELEPHONY\_PROVIDERCHANGE**](https://msdn.microsoft.com/library/windows/hardware/mt169885)電話の呼び出しの種類とプロバイダーの種類を変更する操作を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_テレフォニー\_PROVIDERCHANGE**プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

オーディオ スタックを使用して、 [ **KSTELEPHONY\_PROVIDERCHANGE** ](https://msdn.microsoft.com/library/windows/hardware/mt169885)を開始およびオーディオ ドライバーに SRVCC の末尾を示すプロパティです。 このプロパティは、呼び出しの種類 (LTE パケット交換 WLAN パケット交換または回線交換) を通信し、プロバイダーの変更操作 (開始、終了、またはキャンセル) ドライバーにします。 呼び出しの種類には、プロバイダーの操作が、SRVCC を終了するときは無視されます。

プロバイダーの変更操作の場合は**テレフォニー\_PROVIDERCHANGEOP\_開始**、そのプロバイダーの呼び出しの状態が更新されますドライバー**テレフォニー\_CALLSTATE\_PROVIDERTRANSITION**します。 プロバイダーの変更操作の場合は**テレフォニー\_PROVIDERCHANGEOP\_エンド**、そのプロバイダーの呼び出しの状態が更新されますドライバー**テレフォニー\_CALLSTATE\_有効になっている**します。 SRVCC、中にドライバーが関連付けられているを使用する続ける必要があります[ **KSNODETYPE\_テレフォニー\_BIDI** ](ksnodetype-telephony-bidi.md)エンドポイント、およびそれがこのエンドポイントのジャックの状態を変更していません。 プロバイダーの変更操作の場合は**テレフォニー\_PROVIDERCHANGEOP\_キャンセル**SRVCC がキャンセルされるが、ドライバーは、事前 SRVCC 呼び出しに戻す必要があります。

<a name="requirements"></a>必要条件
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

 

 





