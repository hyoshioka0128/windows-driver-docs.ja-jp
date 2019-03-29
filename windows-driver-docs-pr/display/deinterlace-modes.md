---
title: デインターレース モード
description: デインターレース モード
ms.assetid: 0418ab48-94f3-4914-b07a-ed22dc893544
keywords:
- デインター レースの WDK DirectX va なので、モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621c85b229f6b57f51c778a0148962e85095545d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579970"
---
# <a name="deinterlace-modes"></a>デインターレース モード


## <span id="ddk_deinterlace_modes_gg"></span><span id="DDK_DEINTERLACE_MODES_GG"></span>


DDI でサポートできるインター モードの例を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">モード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="bob-deinterlacing.md" data-raw-source="[Bob](bob-deinterlacing.md)">Bob</a> (行が 2 倍)</p></td>
<td align="left"><p>このモードでは、ビット ブロック転送 (blt) を使用します。 このモードを常に使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>単純なアダプティブの切り替え</p></td>
<td align="left"><p>場合は低モーション検知されて、そのフィールドまたはクリスマス_ツリー高モーションが検出された場合、2 つの隣接するフィールド、blend がいずれか。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>動きベクトルを送る</p></td>
<td align="left"><p>画面で、さまざまなオブジェクトの動きベクトルは、補間に行われる前に個々 の動きを時間軸を整列に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3D の高度なアダプティブ</p></td>
<td align="left"><p>不足している行は、アダプティブのプロセスが、独自のハードウェアを使用して生成されます。 プロセスでは、不足している線の生成を支援するためにいくつかのリファレンス サンプルを使用できます。 過去または将来の参照のサンプルがあります。 3 次元のリニア フィルタ リングは、このカテゴリに分類されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





