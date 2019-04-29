---
title: KSPROPERTY\_テレフォニー\_CALLCONTROL
description: KSPROPERTY\_テレフォニー\_CALLCONTROL プロパティを使用して、起動し、電話の呼び出しを終了します。
ms.assetid: AAC2A218-9A2D-4EFE-B609-5078028B2426
keywords:
- KSPROPERTY_TELEPHONY_CALLCONTROL オーディオ デバイス
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
ms.openlocfilehash: f2498e8864aa0a5ef167ff05c5f80d45012d04a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332606"
---
# <a name="kspropertytelephonycallcontrol"></a>KSPROPERTY\_テレフォニー\_CALLCONTROL


KSPROPERTY\_テレフォニー\_CALLCONTROL プロパティを使用して、起動し、電話の呼び出しを終了します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt169883" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLCONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt169883)"><strong>KSTELEPHONY_CALLCONTROL</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_テレフォニー\_CALLCONTROL プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_テレフォニー\_CALLCONTROL には CallType と CallControlOp に関する情報が含まれています。

テレフォニー\_CALLCONTROLOP\_オーディオ ドライバーの観点から携帯電話の呼び出しを開始が有効にする、更新プログラムのジャック状態に対してアクティブ に移動体通信 bidi エンドポイントに関連付けられた呼び出しの種類を保存し呼び出しの状態を有効に更新します。

テレフォニー\_CALLCONTROLOP\_無効にするにはオーディオ ドライバーの観点から携帯電話の通話を終了、更新プログラムのジャック状態双方向の移動体通信のエンドポイントに関連付けられているの電源が入っていないし、呼び出しの状態の更新を無効にします。 呼び出しの種類は、ここでは無視されます。

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

 

 





