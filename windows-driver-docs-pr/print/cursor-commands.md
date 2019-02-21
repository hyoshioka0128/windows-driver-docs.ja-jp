---
title: カーソル コマンド
description: カーソル コマンド
ms.assetid: 3ef09c7e-0e88-4236-a4c9-d89eb7ec61cb
keywords:
- プリンターが WDK Unidrv、カーソルをコマンドします。
- カーソルの WDK Unidrv コマンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4825df7d9d8f129854e415c1ad3b05796ed09d54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529819"
---
# <a name="cursor-commands"></a>カーソル コマンド





[プリンター コマンド](printer-commands.md)で次のテーブル コントロールのカーソル移動します。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdBackSpace</strong></p></td>
<td><p>印刷の最後の文字に戻るカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 重ね打ちにのみ使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdCR</strong></p></td>
<td><p>左端の x 位置にカーソルを移動するコマンドです。</p></td>
<td><p>必須。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdFF</strong></p></td>
<td><p>ページを取り出すコマンド。</p></td>
<td><p>必須。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdLF</strong></p></td>
<td><p>次の行にカーソルを移動するコマンドです。</p></td>
<td><p>必須。 移動量が指定された<strong>CmdSetLineSpacing</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdPopCursor</strong></p></td>
<td><p>スタックから最後の保存済みのカーソル位置を表示するコマンドです。</p></td>
<td><p>場合に、必ず<strong>CmdPushCursor</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdPushCursor</strong></p></td>
<td><p>現在のカーソル位置をスタックにプッシュするコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetAnyRotation</strong></p></td>
<td><p>(反時計回りに度数で測定) 任意の角度に回転を設定するコマンドです。</p></td>
<td><p>(省略可能)。 存在しない場合、プリンターは、任意の角度で回転をサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetLineSpacing</strong></p></td>
<td><p>カーソルまでの距離を設定するコマンドには、ときに移動します、 <strong>CmdLF</strong>コマンドを発行します。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetSimpleRotation</strong></p></td>
<td><p>反時計回りに 90 ° の倍数での回転角度を設定するコマンドです。</p></td>
<td><p>(省略可能)。 プリンターには、任意のサイズの角度で回転がサポートしている場合、 <strong>CmdSetAnyRotation</strong>コマンドは、このコマンドを置き換えることができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUniDirectionOff</strong></p></td>
<td><p>双方向印刷できるように、一方向の印刷を無効にするコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUniDirectionOn</strong></p></td>
<td><p>一方向の印刷を有効にするコマンドです。</p></td>
<td><p>(省略可能)。 いない場合は、表示、双方向のモードで印刷されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveAbsolute</strong></p></td>
<td><p>絶対の x 位置にカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdXMoveRelLeft</strong></p></td>
<td><p>指定した量 x 位置から、カーソルを左に移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveRelRight</strong></p></td>
<td><p>指定した量によって、x 位置から、右側にカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveAbsolute</strong></p></td>
<td><p>絶対の y 位置にカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdYMoveRelDown</strong></p></td>
<td><p>指定した量によって y 位置からカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveRelUp</strong></p></td>
<td><p>指定した量の y 位置からカーソルを移動するコマンドです。</p></td>
<td><p>(省略可能)。 コマンド文字列には、標準的な変数が 1 つだけの距離を指定するために使用を含めることができます。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




