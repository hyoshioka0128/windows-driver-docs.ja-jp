---
title: コメントおよび無視されたブロック
description: コメントおよび無視されたブロック
ms.assetid: 8b3a0195-b2c8-491d-abcd-bfaebefbc77d
keywords:
- GPD ファイル エントリ WDK Unidrv、無視されたブロック
- WDK GPD ファイルのブロックを無視
- GPD ファイル エントリ WDK Unidrv、コメント
- WDK GPD ファイルのコメント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5ec203052bfbd6368228c32786f28138342ff09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539535"
---
# <a name="comments-and-ignored-blocks"></a>コメントおよび無視されたブロック





GPD ファイルは、コメントを含めることができます。 コメントの形式は次のとおりです。

**\*%** *CommentString*

場所*CommentString*は行終端記号で終わる文字の任意の文字列です。 複数行コメントの各行の先頭、 **\* %** 文字のシーケンス。 **\* %** シーケンスの前に空白または改行でする必要があります。

有効なコメントの例を次に示します。

```cpp
*% This section of the GPD file
*% contains macro definitions.
*Macros: HP4L
{
    *% These macros define command prefixes for the paper size feature.
    LetterCmdPrefix: "<1B>&l2a8c1E<1B>*p0x0Y"  *% Prefix for letter option.
    A4CmdPrefix: "<1B>&l26a8c1E<1B>*p0x0Y"     *% Prefix for A4 option.
    Env10CmdPrefix: "<1B>&l81a8c1E<1B>*p0x0Y"  *% Prefix for Env10 option.
}
```

GPD エントリのグループを無視する GPD パーサーを要求するには、無視するエントリを含むブロックを無視を作成できます。 無視のブロックの形式は次のとおりです。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>*IgnoreBlock</strong> { <em>IgnoredEntries</em> }</p></td>
</tr>
</tbody>
</table>

 

場所*IgnoredEntries*は同じ数の左と右中かっこを含む、GPD ファイル エントリのセットです。

次の例では、ランドス ケープを記述する GPD エントリは無視 GPD パーサー\_CC90 オプション。

```cpp
*Feature: Orientation
{
    *Name: "Orientation"
    *DefaultOption: Portrait
    *Option: Portrait
    {
        *Name: "Portrait"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l0O"
        }
    }
*IgnoreBlock
{
    *Option: LANDSCAPE_CC90
    {
        *Name: "Landscape"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l1O"
        }
    }
}
}
```

 

 




