---
title: コマンド エントリの形式
description: コマンド エントリの形式
ms.assetid: f2b14c12-3c34-45b2-9ead-8cd57d657e9e
keywords:
- プリンターは、WDK Unidrv、エントリの形式をコマンドします。
- WDK プリンター コマンドの形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6a4734f4555ecfe543cdcfc11b01891806f9e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560938"
---
# <a name="command-entry-format"></a>コマンド エントリの形式





GPD ファイルでプリンター コマンドの入力を指定するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* コマンド</strong>:<em>CommandName</em> {<em>CommandAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

場所*CommandName*は定義済みの 1 つ[コマンド名](command-names.md)と*CommandAttributes*は一連の[属性をコマンド](command-attributes.md)します。

たとえば、GPD ファイルには、印刷用ページを初期化する CmdStartPage コマンドの次の仕様が含まれます。

```cpp
*Command: CmdStartPage
{
    *Order: PAGE_SETUP.100
    *Cmd: "<0D>"
}
```

特定の場合、 *CommandName*値のみ指定する必要が、 \*Cmd 属性では、次のように、コマンド入力形式の短縮バージョンを使用することができます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* コマンド</strong>:<em>CommandName</em>:<em>クラスヒント</em></p></td>
</tr>
</tbody>
</table>

 

場所*クラスヒント*プリンター コマンドのエスケープ シーケンスを表す文字列です。 エスケープ シーケンスを指定する方法については、[コマンド文字列の形式](command-string-format.md)を参照してください。

たとえば、GPD ファイルには、太字のテキストをオンにする CmdBoldOn コマンドの次の仕様が含まれます。

```cpp
*Command: CmdBoldOn: "<1B>(s3B"
```

 

 




