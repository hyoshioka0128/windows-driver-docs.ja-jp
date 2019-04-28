---
title: GDL ブロック マクロ
description: GDL ブロック マクロ
ms.assetid: c8b8e38d-237f-4c54-a394-148d211237ce
keywords:
- GDL WDK、マクロ
- マクロ WDK GDL、ブロック マクロ
- WDK GDL マクロをブロックします。
- BlockMacros ディレクティブ WDK GDL
- マクロ WDK GDL、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e83cae8aa82e517d0e39c17d8a86dd23d55466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363188"
---
# <a name="gdl-block-macros"></a>GDL ブロック マクロ


*マクロ ブロック*GDL の 1 つまたは複数のエントリを表すために使用します。 定義されている、 \*BlockMacros を構築します。

インスタンス名、 \*BlockMacros コンス トラクター ブロック マクロ、およびの中かっこ内に含まれるエントリの名前になります、 \*BlockMacros コンストラクトがそのブロックのマクロの内容になります。 マクロ名は、シンボル名の種類である必要があります。 ブロックのマクロ定義に含まれるエントリは、完了する必要があります。

コンストラクトのすべてのエントリがある場合は、マクロ定義内で完了する必要があります。 つまり、ブロックのマクロ定義の内容は、入れ子のレベルを変更することはできません。

ブロックのマクロには、他のブロックまたは値マクロ定義と通常のデータ エントリだけでなく、名前空間ディレクティブを含めることができます。 入れ子になったマクロ定義と名前空間ディレクティブすぐに評価され、ブロック マクロの内容には表示されません。

ブロックのマクロは、その他のブロックまたは値マクロへの参照を含めることができます。 インスタンス名、 \*BlockMacros コンストラクトをかっこで囲まれた仮引数リストが続くことができます。 このブロックのマクロ定義の本体内の任意の仮引数への参照はシンボル ブロック マクロが実際に参照されているときに渡される対応するパラメーターで置き換えられます。

**注**  宣言と値のマクロの参照を渡すために使用される引数の参照が引数の型が値マクロであることを示すに等号 (=) でプレフィックスとして付加されます。 マクロの値に対するすべての参照では、参照がブロック マクロではなく値マクロを示すために等号 (=) もが付きます。

 

ブロック マクロへの参照には、任意の深さのパラメーター リストが入れ子にできます。 使用してブロック マクロが参照されている\*InsertBlock:NameOfBlockMacro します。 ブロック マクロの名前が付いていない等号値マクロへの参照ではないためです。 この構文は、GPD 構文によって異なります。

次のコード例では、ブロックのマクロを使用する方法を示します。

```cpp
*Macros:
{
  LetterName: Letter
  Quote: <BeginValue:Q>"<EndValue:Q>
}
*BlockMacro: LetterSize
{
*Name: =Quote=LetterName=Quote
  *PaperDimension:  PAIR(8.5 , 11)
}
*BlockMacro: PaperOption(PaperSize, =PaperName)
{
  *Option: =PaperName
  {
    *InsertBlock: PaperSize
  }
}

*InsertBlock: PaperOption(LetterSize, =LetterName)
```

 

 




