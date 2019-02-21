---
title: WIA\_DPS\_表示\_プレビュー\_コントロール
description: WIA\_DPS\_表示\_プレビュー\_コントロール プロパティは、項目が、ユーザーに表示されるプレビュー コントロールを必要があるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 45bd6030-34b1-466b-b594-e7ee0d2902f9
keywords:
- WIA_DPS_SHOW_PREVIEW_CONTROL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_SHOW_PREVIEW_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2efaac3e83ff8d8a8a5b05100282260c8299a778
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553039"
---
# <a name="wiadpsshowpreviewcontrol"></a>WIA\_DPS\_表示\_プレビュー\_コントロール


WIA\_DPS\_表示\_プレビュー\_コントロール プロパティは、項目が、ユーザーに表示されるプレビュー コントロールを必要があるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dps_show_preview_control_si"></span><span id="DDK_WIA_DPS_SHOW_PREVIEW_CONTROL_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表に、WIA で有効な定数\_DPS\_表示\_プレビュー\_コントロール。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DONT_SHOW_PREVIEW_CONTROL</p></td>
<td><p>表示しないプレビュー コントロールをユーザーにこのデバイスはプレビューを実行できないためです。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SHOW_PREVIEW_CONTROL</p></td>
<td><p>このデバイスは、プレビューを実行できるため、ユーザーにプレビュー コントロールを表示します。</p></td>
</tr>
</tbody>
</table>

 

WIA\_DPS\_表示\_プレビュー\_コントロール プロパティをプレビューできませんデバイスの制御に役立ちます。 たとえば、フィーダー駆動の一部のデバイスには、プレビュー スキャンのホワイト ペーパーが再読み込みできません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP で利用できます。 ForWindows Vista し、後で WIA_IPS_SHOW_PREVIEW_CONTROL プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IP\_表示\_プレビュー\_コントロール**](wia-ips-show-preview-control.md)

 

 






