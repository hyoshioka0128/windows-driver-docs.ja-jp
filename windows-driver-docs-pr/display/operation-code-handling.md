---
title: 操作コードの処理
description: 操作コードの処理
ms.assetid: 97de8370-316e-41df-bf27-1985af47a4e0
keywords:
- Direct3D WDK Windows 2000 の表示、操作コード
- 操作コード WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 957821ee5d85e1ad0f191daac26066b8b87beea1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370636"
---
# <a name="operation-code-handling"></a>操作コードの処理


## <span id="ddk_opcode_handling_gg"></span><span id="DDK_OPCODE_HANDLING_GG"></span>


ディスプレイ ドライバーはグラフィックスのプリミティブとプロセスの状態の変化を表示するために要求を処理、 [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 ドライバーがこれらの要求を受信[ **D3DHAL\_DP2OPERATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)オペレーション コード。 次のトピックでは、ドライバーが操作のコードを処理する方法と、このような処理中に、パフォーマンスを向上する方法について説明します。

[コマンド Stream](command-stream.md)

[操作の処理のパフォーマンスを向上させる](improving-performance-of-operation-handling.md)

ドライバー作成者を Microsoft DirectX 7.0 およびそれ以降の Direct3D ドライバー モデルをサポートするためには、そのドライバーの実装で、新しい操作コードの数値に対応させる必要があります[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb). これらの操作コードの一部の置換コールバック関数、および他のユーザーが新しい機能を提供します。 最も重要な新しいオペレーション コードは、以降のコールバックを置き換えるものでは、次の表にまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作コード</th>
<th align="left">条件/説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETRENDERTARGET</p></td>
<td align="left"><p><strong>常に必要です。</strong> 新しいレンダリング ターゲット画面と深度バッファーを現在のコンテキストでマップされます。 置換<em>D3dSetRenderTarget</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_CLEAR</p></td>
<td align="left"><p><strong>常に必要です。</strong> コンテキストのレンダー ターゲット、Z バッファーをクリアするために使用します。 置換<em>D3dClear2</em>します。 ハードウェアのステンシル バッファーと深度の塗りつぶしのビット ブロック転送を適切に消去できません深度バッファーをクリアするも使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETPALETTE</p></td>
<td align="left"><p>パレットのハンドルとサーフェスのハンドル、間のアソシエーションをマップし、パレットの特性を指定するために使用します。 パレット化されたテクスチャをサポートするドライバーに対してのみ必要です。それ以外の場合このことはありません (NOP) 操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_UPDATEPALETTE</p></td>
<td align="left"><p>パレット化されたテクスチャをサポートするドライバーに対して、テクスチャ パレットを変更するために使用します。 それ以外の場合、NOP があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_TEXBLT</p></td>
<td align="left"><p>転送先のテクスチャをソース テクスチャから blt 操作を指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





