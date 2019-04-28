---
title: パスの GDI サービス
description: パスの GDI サービス
ms.assetid: 8fc51b7e-d787-48ed-a865-528547abefc5
keywords:
- GDI WDK Windows 2000 の表示パス
- グラフィックス ドライバー WDK Windows 2000 の表示、パス
- WDK の GDI やパスの描画
- WDK GDI のパス
- WDK GDI のパスを入力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cb464f3a1b384e1aa6be90b0f7a1c45927b1f2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371562"
---
# <a name="gdi-services-for-paths"></a>パスの GDI サービス


## <span id="ddk_gdi_services_for_paths_gg"></span><span id="DDK_GDI_SERVICES_FOR_PATHS_GG"></span>


複雑な領域がいっぱいのベクターのデバイスを支援するために、ドライバーことができます関数を呼び出す、エンジン、次の表では、作成、変更、およびパスを列挙します。 ドライバーを経由するパスへのアクセス、 [ **PATHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff568849)構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GDI Path サービス関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564755" data-raw-source="[&lt;strong&gt;EngCreatePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564755)"><strong>EngCreatePath</strong></a></p></td>
<td align="left"><p>ドライバーの一時使用するためのパスを割り当てます。 ドライバーは、その現在の描画呼び出しから GDI に戻る前にこのパスを削除する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564811" data-raw-source="[&lt;strong&gt;EngDeletePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564811)"><strong>EngDeletePath</strong></a></p></td>
<td align="left"><p>によって割り当てられたパスを削除、 <strong>EngCreatePath</strong>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568850" data-raw-source="[&lt;strong&gt;PATHOBJ_bCloseFigure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568850)"><strong>PATHOBJ_bCloseFigure</strong></a></p></td>
<td align="left"><p>行を開始位置に描画して (塗りつぶし) のパスを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568851" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568851)"><strong>PATHOBJ_bEnum</strong></a></p></td>
<td align="left"><p>次の取得<a href="https://msdn.microsoft.com/library/windows/hardware/ff568848" data-raw-source="[&lt;strong&gt;PATHDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568848)"> <strong>PATHDATA</strong> </a>パスからレコード。 各レコードは、下位のすべてまたは一部について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568852" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnumClipLines&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568852)"><strong>PATHOBJ_bEnumClipLines</strong></a></p></td>
<td align="left"><p>パスからクリップされた線セグメントを列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568853" data-raw-source="[&lt;strong&gt;PATHOBJ_bMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568853)"><strong>PATHOBJ_bMoveTo</strong></a></p></td>
<td align="left"><p>内の現在位置を変更、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568849" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568849)"> <strong>PATHOBJ</strong></a>-パスを定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568854" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyBezierTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568854)"><strong>PATHOBJ_bPolyBezierTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定義のパスでは、(3 次スプライン) のベジエ曲線を描画します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568855" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568855)"><strong>PATHOBJ_bPolyLineTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定義のパスの線を描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568856" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568856)"><strong>PATHOBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>通知を<a href="https://msdn.microsoft.com/library/windows/hardware/ff568849" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568849)"> <strong>PATHOBJ</strong> </a>ドライバーが通話を開始する<strong>PATHOBJ_bEnum</strong>指定されたパス内の曲線を列挙します。 列挙に再起動が発生した場合は、この関数を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568857" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStartClipLines&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568857)"><strong>PATHOBJ_vEnumStartClipLines</strong></a></p></td>
<td align="left"><p>により、行に対してクリップすることを要求するドライバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff539417" data-raw-source="&lt;strong&gt;CLIPOBJ&lt;/strong&gt;"><em>クリップ領域</em></a> 1 つの四角形よりも複雑です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568858" data-raw-source="[&lt;strong&gt;PATHOBJ_vGetBounds&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568858)"><strong>PATHOBJ_vGetBounds</strong></a></p></td>
<td align="left"><p>パスの外接する四角形を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





