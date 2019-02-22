---
title: モノクロ ポインターの描画
description: モノクロ ポインターの描画
ms.assetid: b3e436d2-b804-42fb-89ca-ecf66dcb584e
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- モノクロ ポインター WDK Windows 2000 を表示します。
- 白黒ポインター WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24695499781b378d0a57e6c045c786ab53d075f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553005"
---
# <a name="drawing-monochrome-pointers"></a>モノクロ ポインターの描画


## <span id="ddk_drawing_monochrome_pointers_gg"></span><span id="DDK_DRAWING_MONOCHROME_POINTERS_GG"></span>


モノクロ ビットマップは、2 つの部分で構成されています最初のポインター。 AND マスクを定義します。2 つ目は、XOR マスクを定義します。 これらこれらのマスクは、2 つのビットのポインターの画像のピクセルごとの情報を提供できます。 次の表に、AND で指定された値に対して表示される結果と XOR マスク。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マスクの値と</th>
<th align="left">XOR マスクの値</th>
<th align="left">結果が表示されます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ピクセルは黒</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ピクセルは白</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ピクセルの (透明) は変更されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ピクセルの色を反転します。</p></td>
</tr>
</tbody>
</table>

 

このビットマップ定義と使用法の透過性と、ポインターを構成するピクセルの反転のサポートを提供しながら、白黒のイメージを提供します。

 

 





