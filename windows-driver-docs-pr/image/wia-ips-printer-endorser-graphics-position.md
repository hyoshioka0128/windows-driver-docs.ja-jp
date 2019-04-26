---
title: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_位置
description: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_POSITION プロパティはテキスト コンテンツの印刷動作保証済みの基準とした (グラフィックス) イメージの位置を構成に使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: CB7B84F0-A585-49AB-ADDE-039C2D415E72
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_POSITION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_POSITION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 657f8ed9931624b1a7ef80d08dd555d844c735ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352092"
---
# <a name="wiaipsprinterendorsergraphicsposition"></a>WIA\_IP\_プリンター\_裏書き\_グラフィックス\_位置


**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_位置**プロパティを使用して、テキスト コンテンツを基準として (グラフィックス) イメージの位置を構成します。印刷動作保証するには。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表では有効な定数**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_位置**します。

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
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_LEFT</p></td>
<td><p>イメージが印刷/動作保証済みの左側にある、・ インプリント ・/裏書き領域の。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RIGHT</p></td>
<td><p>イメージが印刷/動作保証済みの右側にある、・ インプリント ・/裏書き領域の。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP</p></td>
<td><p>イメージが印刷/動作保証済みの上部にある、・ インプリント ・/裏書き領域の。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM</p></td>
<td><p>イメージが印刷/動作保証済みの下部にある、・ インプリント ・/裏書き領域の。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_LEFT</p></td>
<td><p>イメージは、印刷/動作保証済み・ インプリント ・/裏書き領域の左上隅にあります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_RIGHT</p></td>
<td><p>イメージは、印刷/動作保証済み・ インプリント ・/裏書き領域の右上隅にあります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_LEFT</p></td>
<td><p>イメージは、印刷/動作保証済み・ インプリント ・/裏書き領域の左下隅にあります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_RIGHT</p></td>
<td><p>イメージは、印刷/動作保証済み・ インプリント ・/裏書き領域の右下隅にあります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BACKGROUND</p></td>
<td><p>イメージが印刷/動作保証済みの背景として、テキストは印刷動作保証済みイメージの上。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RANDOM</p></td>
<td><p>イメージは、デバイスによって選択されたランダムな位置にある印刷動作保証済み。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_ GRAPHICS_DEVICE_DEFAULT</p></td>
<td><p>イメージは、デバイスが選択した既定 (推奨) の位置にある印刷動作保証済み。</p></td>
</tr>
</tbody>
</table>

 

WIA\_プリンター\_裏書き\_グラフィックス\_デバイス\_既定値は、必要な既定値・ インプリント ・/裏書きのすべての項目には、このプロパティがサポートされている場合をサポートする必要があります。

このプロパティは、必要なの 0 以外の値 (True) の値を報告するすべての・ インプリント ・/裏書き項目に対して有効な[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス**](wia-ips-printer-endorser-graphics.md). プロパティはそれ以外の場合有効ではありません。

<a name="requirements"></a>必要条件
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

 

 





