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
ms.openlocfilehash: 26da52fcfa7359513615bd9a10bd7eba1d4ebb5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354722"
---
# <a name="gdi-services-for-paths"></a>パスの GDI サービス


## <span id="ddk_gdi_services_for_paths_gg"></span><span id="DDK_GDI_SERVICES_FOR_PATHS_GG"></span>


複雑な領域がいっぱいのベクターのデバイスを支援するために、ドライバーことができます関数を呼び出す、エンジン、次の表では、作成、変更、およびパスを列挙します。 ドライバーを経由するパスへのアクセス、 [ **PATHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)構造体。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath" data-raw-source="[&lt;strong&gt;EngCreatePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath)"><strong>EngCreatePath</strong></a></p></td>
<td align="left"><p>ドライバーの一時使用するためのパスを割り当てます。 ドライバーは、その現在の描画呼び出しから GDI に戻る前にこのパスを削除する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepath" data-raw-source="[&lt;strong&gt;EngDeletePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepath)"><strong>EngDeletePath</strong></a></p></td>
<td align="left"><p>によって割り当てられたパスを削除、 <strong>EngCreatePath</strong>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure" data-raw-source="[&lt;strong&gt;PATHOBJ_bCloseFigure&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bclosefigure)"><strong>PATHOBJ_bCloseFigure</strong></a></p></td>
<td align="left"><p>行を開始位置に描画して (塗りつぶし) のパスを閉じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnum&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum)"><strong>PATHOBJ_bEnum</strong></a></p></td>
<td align="left"><p>次の取得<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathdata" data-raw-source="[&lt;strong&gt;PATHDATA&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathdata)"> <strong>PATHDATA</strong> </a>パスからレコード。 各レコードは、下位のすべてまたは一部について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_bEnumClipLines&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benumcliplines)"><strong>PATHOBJ_bEnumClipLines</strong></a></p></td>
<td align="left"><p>パスからクリップされた線セグメントを列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto" data-raw-source="[&lt;strong&gt;PATHOBJ_bMoveTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bmoveto)"><strong>PATHOBJ_bMoveTo</strong></a></p></td>
<td align="left"><p>内の現在位置を変更、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)"> <strong>PATHOBJ</strong></a>-パスを定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyBezierTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolybezierto)"><strong>PATHOBJ_bPolyBezierTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定義のパスでは、(3 次スプライン) のベジエ曲線を描画します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto" data-raw-source="[&lt;strong&gt;PATHOBJ_bPolyLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_bpolylineto)"><strong>PATHOBJ_bPolyLineTo</strong></a></p></td>
<td align="left"><p>PATHOBJ 定義のパスの線を描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStart&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart)"><strong>PATHOBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>通知を<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)"> <strong>PATHOBJ</strong> </a>ドライバーが通話を開始する<strong>PATHOBJ_bEnum</strong>指定されたパス内の曲線を列挙します。 列挙に再起動が発生した場合は、この関数を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines" data-raw-source="[&lt;strong&gt;PATHOBJ_vEnumStartClipLines&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstartcliplines)"><strong>PATHOBJ_vEnumStartClipLines</strong></a></p></td>
<td align="left"><p>により、行に対してクリップすることを要求するドライバー、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="&lt;strong&gt;CLIPOBJ&lt;/strong&gt;"><em>クリップ領域</em></a> 1 つの四角形よりも複雑です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds" data-raw-source="[&lt;strong&gt;PATHOBJ_vGetBounds&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_vgetbounds)"><strong>PATHOBJ_vGetBounds</strong></a></p></td>
<td align="left"><p>パスの外接する四角形を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





