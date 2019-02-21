---
title: WIA\_IP\_色\_ドロップ
description: WIA\_IP\_色\_ドロップ プロパティを使用して、ハードウェア デバイスから取得したイメージ データのフィルター処理する色を構成します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: A0F14FDF-194D-4948-B9D8-F3E0C2E34618
keywords:
- WIA_IPS_COLOR_DROP イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4186e43792528d14a3629ae1c76cb5cfb1f09379
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537930"
---
# <a name="wiaipscolordrop"></a>WIA\_IP\_色\_ドロップ


**WIA\_IP\_色\_ドロップ**プロパティを使用して、ハードウェア デバイスから取得したイメージ データのフィルター処理する色を構成します。 WIA ミニドライバーは、作成し、このプロパティを保持します。



プロパティの種類:VT\_I4 

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_色\_ドロップ**プロパティ。

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
<td><p>WIA_COLOR_DROP_DISABLED</p></td>
<td><p>色 が無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_RED</p></td>
<td><p>説明されている時間内に赤チャネルが削除される<a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"> <strong>WIA_IPS_COLOR_DROP_RED</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_GREEN</p></td>
<td><p>説明されている量で緑チャネルが削除される<a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"> <strong>WIA_IPS_COLOR_DROP_GREEN</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_BLUE</p></td>
<td><p>説明されている金額に青のチャネルが削除される<a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"> <strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_RGB</p></td>
<td><p>指定された量で、赤、緑、および青のチャネルが削除されます<a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"> <strong>WIA_IPS_COLOR_DROP_RED</strong></a>、 <a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"> <strong>WIA_IPS_COLOR_DROP_GREEN</strong> </a>、および<a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"> <strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、フラット ベッドを含むすべてプログラミング可能なイメージのデータ ソース アイテムの有効な (WIA\_カテゴリ\_ベッド) とフィーダー (WIA\_カテゴリ\_フィーダー) は省略可能です。 プロパティがサポートされている、WIA\_色\_ドロップ\_無効になっていますが、必要な既定値。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





