---
title: ブロック マクロ
description: ブロック マクロ
ms.assetid: da2f6161-072a-4d3c-94a8-1020520de524
keywords:
- ブロック マクロ WDK GPD ファイル
- マクロを参照します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2907bf99f495a6a691acbeeb876bbec24f3bbf83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348498"
---
# <a name="block-macros"></a>ブロック マクロ





ブロックのマクロは、繰り返し GPD ファイルに挿入する GPD ファイル エントリのセットを区切るために使用されます。 機能とオプションのステートメント、属性の仕様、および値マクロまたはその他のブロック マクロへの参照など、ブロックのマクロ定義内のエントリの種類を含めることができます。

次の規則は、ブロックのマクロの使用に適用されます。

-   GPD ファイル内でブロック マクロ定義への参照を任意の前にある必要があります。

-   ルート レベルで定義されているブロック マクロ (つまり、中かっこ内ではなく) を定義している、定義後 GPD ファイルを通じて利用できます。 それ以外の場合、マクロ ブロックのスコープは、その定義を含む左と右かっこのセットです。

-   ブロックのマクロ定義では、追加のブロックのマクロとマクロの値の定義を含めることができます。

-   他のブロックを以前に定義されたマクロと値のマクロ ブロックのマクロ定義を参照できますが、これ自体は参照できません。

-   ブロックのマクロは引数を受け入れません。

-   中かっこがマクロの本体に含まれている場合、ペアリングする必要があります (つまり、必要があります左と右中かっこの数が等しい)。

-   同じ名前の 2 つのブロック マクロを作成する場合、最初の定義が有効で GPD パーサーが 2 番目の定義を検出するまで。 2 番目の定義には、最初が置き換えられます。 2 番目の定義のスコープが終了した場合は、最初の定義が再開されます。

### <a name="block-macro-format"></a>ブロックのマクロの形式

GPD ファイル ブロック マクロを定義するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>BlockMacro</strong>:<em>BlockMacroName</em> {<em>BlockMacroBody</em>}</p></td>
</tr>
</tbody>
</table>

 

場所*BlockMacroName*一意の名前を指定すると*BlockMacroBody*は 1 つまたは複数のセットです[GPD ファイル エントリ](gpd-file-entries.md)します。 場合*BlockMacroBody* 、中かっこが含まれていますと同じ数の左と右中かっこ ({、}) を含める必要があります。

たとえば、EnvelopeDefaults、次のように定義されている名前付きブロック マクロを定義する場合があります。

```cpp
*BlockMacro: EnvelopeDefaults
{
    *PrintableArea: PAIR(4646, 6738)
    *PrintableOrigin: PAIR(150, 150)
    *RotateSize: TRUE
}
```

### <a name="referencing-block-macros"></a>参照元のブロック マクロ

ブロックのマクロを参照するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* InsertBlock</strong>: BlockMacroName を =</p></td>
</tr>
</tbody>
</table>

 

場所*BlockMacroName*に指定されている、一意の名前、  **\*BlockMacro**マクロを定義するエントリ。

たとえば、オプションの指定に EnvelopeDefaults マクロを参照するには、次のエントリを使用できます。

```cpp
*Option: Env9
{
    *InsertBlock: =EnvelopeDefaults
}
```

 

 




