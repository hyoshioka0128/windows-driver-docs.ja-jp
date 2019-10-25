---
title: 操作コードの処理
description: 操作コードの処理
ms.assetid: 97de8370-316e-41df-bf27-1985af47a4e0
keywords:
- Direct3D WDK Windows 2000 display、操作コード
- 操作コード WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd7ed5c7aaae8d0021529099d4749ca908c4ae26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840499"
---
# <a name="operation-code-handling"></a>操作コードの処理


## <span id="ddk_opcode_handling_gg"></span><span id="DDK_OPCODE_HANDLING_GG"></span>


ディスプレイドライバーは、グラフィックスプリミティブのレンダリング要求を処理し、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数での状態の変更を処理します。 ドライバーは、これらの要求を[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作コードとして受信します。 次のトピックでは、ドライバーが操作コードを処理する方法と、その処理中にパフォーマンスを向上させる方法について説明します。

[コマンドストリーム](command-stream.md)

[操作処理のパフォーマンスの向上](improving-performance-of-operation-handling.md)

Microsoft DirectX 7.0 以降の Direct3D ドライバーモデルをサポートするために、ドライバーの作成者は、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)の実装に含まれるさまざまな新しい操作コードにドライバーを応答させる必要があります。 これらの操作コードの中には、コールバック関数を置き換えるものと、新しい機能を提供するものがあります。 次の表に、コールバックを置き換える最も重要な新しい操作コードをまとめて示します。

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
<td align="left"><p><strong>常に必要です。</strong> 新しいレンダリングターゲットサーフェイスと深度バッファーを現在のコンテキストにマップします。 <em>D3dSetRenderTarget</em>を置き換えます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_CLEAR</p></td>
<td align="left"><p><strong>常に必要です。</strong> コンテキストのレンダーターゲットである Z バッファーをクリアするために使用されます。 <em>D3dClear2</em>を置き換えます。 ハードウェアのステンシルバッファー、および深度の fill ビットブロック転送によって適切にクリアできない深度バッファーをクリアするためにも使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_SETPALETTE</p></td>
<td align="left"><p>パレットハンドルとサーフェイスハンドルの間の関連付けをマップし、パレットの特性を指定するために使用します。 パレット化されたテクスチャをサポートするドライバーにのみ必要です。それ以外の場合は、操作 (NOP) ではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DDP2OP_UPDATEPALETTE</p></td>
<td align="left"><p>テクスチャパレットを変更するために使用します。テクスチャパレットは、パレット化されたテクスチャをサポートするドライバー用です。 それ以外の場合は、NOP である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DDP2OP_TEXBLT</p></td>
<td align="left"><p>ソーステクスチャから宛先テクスチャへの blt 操作を指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





