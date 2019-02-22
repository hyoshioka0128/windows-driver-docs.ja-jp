---
title: アルファ ブレンドの組み合わせ
description: アルファ ブレンドの組み合わせ
ms.assetid: 567810da-ad8d-4ceb-b914-868632384d09
keywords:
- アルファ ブレンド WDK DirectX VA の組み合わせ
- WDK DirectX VA ブレンドの画像
- アルファ ブレンド アルファ ブレンドの組み合わせについて、組み合わせ WDK DirectX va なので、
- ブレンド画像アルファ ブレンドの組み合わせの詳細については、WDK DirectX va なので、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2689975c2d301be5c5b547d35404a910dc077c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529809"
---
# <a name="alpha-blend-combination"></a>アルファ ブレンドの組み合わせ


## <span id="ddk_alpha_blend_combination_gg"></span><span id="DDK_ALPHA_BLEND_COMBINATION_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)は 3 に等しく、指定された操作は、アルファ ブレンドの組み合わせ。 アルファ ブレンドの組み合わせは、最後に読み込まれたアルファ ブレンド ソース情報を受け取り、表示の画像を組み合わせたを作成する参照の画像を使用して、それを結合します。

指定したアルファ ブレンドの組み合わせのバッファー、 **dwTypeIndex**のメンバー、 [ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)構造を使用して、混合型の生成ソース画像とアルファ ブレンドの情報の画像。 4 ではない送信元と送信先の画像を: 4:4 の書式設定、すべて、AYUV アルファ ブレンド画面またはそれと同等の情報を描画するグラフィックの (例、最初、3 番目、5 番目、およびなど) の 2 つ目のサンプルは、(低い解像度に適用されます) ソース組み合わせた結果を生成するために、該当すると、水平または垂直方向にクロミナンス情報。

次の構造は、アルファ ブレンドの組み合わせを実装するために使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563122" data-raw-source="[&lt;strong&gt;DXVA_BufferDescription&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563122)"><strong>DXVA_BufferDescription</strong></a></p></td>
<td align="left"><p>使用するアルファ ブレンドの組み合わせのバッファーを指定します。 このバッファーは、ソースの画像とアルファ ブレンド情報から画像を組み合わせたの生成を制御します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563120" data-raw-source="[&lt;strong&gt;DXVA_BlendCombination&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563120)"><strong>DXVA_BlendCombination</strong></a></p></td>
<td align="left"><p>アルファ ブレンドの組み合わせ、バッファーからのブレンドされた画像を生成する方法を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563126" data-raw-source="[&lt;strong&gt;DXVA_ConfigAlphaCombine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563126)"><strong>DXVA_ConfigAlphaCombine</strong></a></p></td>
<td align="left"><p>構成を確立する操作はアルファ ブレンディングの組み合わせを実行します。</p></td>
</tr>
</tbody>
</table>

 

 

 





