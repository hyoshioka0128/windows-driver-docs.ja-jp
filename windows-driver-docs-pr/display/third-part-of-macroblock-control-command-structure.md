---
title: マクロブロック制御コマンド構造の 3 番目の部分
description: マクロブロック制御コマンド構造の 3 番目の部分
ms.assetid: 4e378d2f-dbb2-42b6-984e-b231bb806a7c
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5cc5499631a6902954e74a2ea7497bde1431a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829328"
---
# <a name="third-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の 3 番目の部分


## <span id="ddk_third_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_THIRD_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**b**のメンバーが1の場合、マクロブロックコントロールのコマンド構造は、「[マクロブロックコントロールのコマンド構造」の2番目の部分](second-part-of-macroblock-control-command-structure.md)で説明されているデータで終了します。 **Bare 内部**がゼロの場合、モーション補正プロセスを制御するために、次の追加のデータ要素がマクロブロックコントロールコマンドに含まれています。 次のデータは、 [**DXVA\_MVvalue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue)構造体の配列であり、マクロブロックコントロールのコマンド構造の**mvector**メンバーに含まれています。 **Mvector**内の要素の数は、次の表に示す DXVA\_のメンバーによって指定された画像の種類によって異なります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">B絵文字 Obmc</th>
<th align="left">B絵文字 (Pb)</th>
<th align="left">bPic4MVallowed</th>
<th align="left">MVector 内の要素の数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>11</p></td>
</tr>
</tbody>
</table>

 

*Dxva*ファイルで定義されているマクロブロックコントロール用の**mvector**配列に指定されているモーションベクターの数は4です。これは最も一般的に使用される形式であるためです **。  **

 

 

 





