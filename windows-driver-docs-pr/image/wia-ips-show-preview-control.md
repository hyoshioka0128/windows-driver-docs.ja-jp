---
title: WIA\_IP\_表示\_プレビュー\_コントロール
description: WIA\_IP\_表示\_プレビュー\_コントロール プロパティは、項目が、ユーザーに表示されるプレビュー コントロールを必要があるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 50559dc2-8e5b-4dbc-9c39-8c51e0f825dc
keywords:
- WIA_IPS_SHOW_PREVIEW_CONTROL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SHOW_PREVIEW_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65bf1c747517b843b0d316d3742a8f68446d606d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343830"
---
# <a name="wiaipsshowpreviewcontrol"></a>WIA\_IP\_表示\_プレビュー\_コントロール


WIA\_IP\_表示\_プレビュー\_コントロール プロパティは、項目が、ユーザーに表示されるプレビュー コントロールを必要があるかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表に、WIA で有効な定数\_IP\_表示\_プレビュー\_コントロール。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
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

 

WIA を使用する\_IP\_表示\_プレビュー\_をプレビューできませんデバイスの制御を支援するコントロール プロパティ。 たとえば、フィーダー駆動の一部のデバイスには、プレビュー スキャンのホワイト ペーパーが再読み込みできません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_SHOW_PREVIEW_CONTROL プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_表示\_プレビュー\_コントロール**](wia-dps-show-preview-control.md)

 

 






