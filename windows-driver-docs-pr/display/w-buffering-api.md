---
title: W バッファリング API
description: W バッファリング API
ms.assetid: 7244d697-5200-4d37-9a75-270788c1c7f7
keywords:
- Direct3D WDK Windows 2000 の表示、w バッファリング
- WDK Direct3D の w バッファリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 529757973552366f1b4b08bde1e18748bd296daf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536114"
---
# <a name="w-buffering-api"></a>W バッファリング API


## <span id="ddk_w_buffering_api_gg"></span><span id="DDK_W_BUFFERING_API_GG"></span>


D3DRENDERSTATE\_ZENABLE レンダリング D3DZBUFFERTYPE 列挙型から 3 つの設定を状態がサポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DZB_FALSE</p></td>
<td align="left"><p>すべての深度のバッファリングを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DZB_TRUE</p></td>
<td align="left"><p>Z バッファーを使用する正しいパースペクティブを使用した<em>z</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DZB_USEW</p></td>
<td align="left"><p>Z バッファーを無効にしますが、w バッファリング、視点からの相対であることができます<em>z</em>します。</p></td>
</tr>
</tbody>
</table>

 

格納するため、正確な形式が使用されるため、 *w*ばらつきを不透明にすると想定する必要があります。

画面の割り当てと深さ fill 操作は、w バッファリングを使用する場合と同じ機能です。 すべての z バッファーは、いずれの場合も同じ作業モードを比較します。

詳細については、DirectX SDK のドキュメントを参照してください。

 

 





