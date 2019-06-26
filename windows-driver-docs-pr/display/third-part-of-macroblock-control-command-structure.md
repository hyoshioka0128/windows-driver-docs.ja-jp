---
title: マクロブロック制御コマンド構造の 3 番目の部分
description: マクロブロック制御コマンド構造の 3 番目の部分
ms.assetid: 4e378d2f-dbb2-42b6-984e-b231bb806a7c
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d55c8f7824de90007579792eb04254b78fe3a5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384581"
---
# <a name="third-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の 3 番目の部分


## <span id="ddk_third_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_THIRD_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


場合、 **bPicIntra**のメンバー [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)は 1、で説明されているデータをマクロブロックコントロールコマンドの構造体の終了です。[2 番目のコマンドの構造体をマクロ ブロック コントロールの部分](second-part-of-macroblock-control-command-structure.md)します。 場合**bPicIntra**がゼロにすると、次の追加データ モーションの補正プロセスを制御するマクロ ブロック コントロール コマンド要素が含まれています。 その後のデータの配列は、 [ **DXVA\_MVvalue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_mvvalue)構造体に含まれている、 **MVector**マクロ ブロック コントロール コマンド構造体のメンバー。 要素数**MVector** DXVA のメンバーで指定された画像の種類によって異なります\_PictureParameters 次の表にします。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bPicOBMC</th>
<th align="left">bPicBinPB</th>
<th align="left">bPic4MVallowed</th>
<th align="left">MVector 内の要素の数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
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

 

**注**  で指定した動きベクトルの数、 **MVector** 、マクロ ブロックの配列で定義されているコマンドの構造を制御する、 *dxva.h*ファイルは 4 で、これは、最もよく使用される構造体の形式。

 

 

 





