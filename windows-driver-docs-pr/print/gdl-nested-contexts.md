---
title: GDL 入れ子コンテキスト
description: GDL 入れ子コンテキスト
ms.assetid: c679937a-fa36-487a-84f2-f61a7ef0198e
keywords:
- GDL WDK、コンテキスト
- WDK GDL、入れ子になったコンテキストのコンテキスト
- 入れ子になったコンテキスト WDL GDL
- GDL WDK、値
- WDK GDL、入れ子になったコンテキストを値します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f69092e1e218277bce87e0baf2b9c14ec2b39cba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574218"
---
# <a name="gdl-nested-contexts"></a>GDL 入れ子コンテキスト


A*入れ子になったコンテキスト*がで導入された、*入れ子の文字の開始*(かっこまたは角かっこでは)。 入れ子になったコンテキストは終了、一致する*入れ子の文字の終了*(かっこや閉じ角かっこでは) が発生しました。

入れ子のコンテキストは、互いに入れ子にできます。 現在の入れ子のコンテキストを終了するには、のみ終了入れ子文字を使用できます。 最後の入れ子の文字がその他の場所表示されない場合は、構文エラーです。

入れ子になったコンテキスト内で、[区切り文字を構築](gdl-construct-delimiters.md)区切り記号を構築し、入れ子になったコンテキストの区切り記号としても扱われるようにその意味が失われます。 、入れ子になったコンテキスト内では、linebreak シーケンスは、リテラル以外の空白文字として扱われます。

任意のコンテキストの外部または入れ子になった別のコンテキスト内が他のコンテキスト内ではなく、入れ子になったコンテキストを表示できます。 HexSubString コンテキストを除く、入れ子になったコンテキスト内で入れ子になった他のコンテキストを含む、任意のコンテキストに表示されます。

次のコード例は、GDL 入れ子になったコンテキストを示しています。

```cpp
*good_nests: ( { } [ ( ) ] )
```

次のコード例として示す GDL には、エラーが含まれるコンテキストが入れ子になった。

```cpp
*bad_nests: (  ] *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  ]  )
*bad_nests:   ] [   *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  [  )   ]   *%  end nesting delimiter can only be used within its nesting*% context.  In this case the ')' char cannot be used within the context begun 
*%by '[' .
*bad_nests:  {  [ ]  }  *% attempt to use construct delimiter to define a nesting context 
*%  outside of a nesting context.
```

入れ子になったコンテキストの内容全体がの一部として扱われます、[値](gdl-values.md)します。 たとえば、GDL の次のコードがのキーワードを使用して 1 つのエントリを表します"\*KeywordA"。 フラグメントの残りの部分の値である\*KeywordA、ため、別のエントリに見えるもの\*KeywordB と\*KeywordC が入れ子になったコンテキスト内に含まれます。 実際には、数値に「12、38, 709」自体が、角かっこの区切り記号で定義されている外側のコンテキスト内で入れ子になったかっこの区切り記号で定義されている入れ子になったコンテキスト。

```cpp
*KeywordA: [
*KeywordB:  List(12, 38, 709)
*KeywordC:  "the small brown fox" ]
```

 

 




