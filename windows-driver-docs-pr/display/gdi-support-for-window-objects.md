---
title: ウィンドウ オブジェクトの GDI サポート
description: ウィンドウ オブジェクトの GDI サポート
ms.assetid: 288120e0-e43c-4733-8bba-0e310ed55aae
keywords:
- GDI WDK Windows 2000 の表示、ウィンドウ オブジェクト
- グラフィックス ドライバー WDK Windows 2000 の表示、ウィンドウ オブジェクト
- WDK GDI、ウィンドウ オブジェクトの描画
- ウィンドウ オブジェクトの WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3493aba14b3bb655c1ae23ee31cbccfb52a41fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384463"
---
# <a name="gdi-support-for-window-objects"></a>ウィンドウ オブジェクトの GDI サポート


## <span id="ddk_gdi_support_for_window_objects_gg"></span><span id="DDK_GDI_SUPPORT_FOR_WINDOW_OBJECTS_GG"></span>


GDI は、ウィンドウの作成と削除、およびウィンドウ内の四角形の列挙型のサポートを提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564769" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564769)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>作成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>指定した表面に構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564830" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564830)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>削除、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570602" data-raw-source="[&lt;strong&gt;WNDOBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570602)"><strong>WNDOBJ_bEnum</strong></a></p></td>
<td align="left"><p>ウィンドウの表示領域から四角形のコレクションを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570603" data-raw-source="[&lt;strong&gt;WNDOBJ_cEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570603)"><strong>WNDOBJ_cEnumStart</strong></a></p></td>
<td align="left"><p>ウィンドウの表示領域の四角形の列挙型のパラメーターを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570606" data-raw-source="[&lt;strong&gt;WNDOBJ_vSetConsumer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570606)"><strong>WNDOBJ_vSetConsumer</strong></a></p></td>
<td align="left"><p>ドライバーの定義済みの値を設定、 <strong>pvConsumer</strong>の指定したメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

 

 





