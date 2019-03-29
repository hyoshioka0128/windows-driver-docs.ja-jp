---
title: GDL コンストラクト
description: GDL コンストラクト
ms.assetid: e579bff0-4e28-4e9e-bef2-f6748c3849e5
keywords:
- GDL の WDK を構築します
- WDK GDL を構築します。
- 子エントリ WDK GDL
- 親コンストラクト WDK GDL
- 先祖コンストラクト WDK GDL
- WDK GDL の構文構造
- WDK GDL の論理構造
- WDK GDL 共用体
- WDK GDL、構文構造を構築します。
- WDK GDL、論理構造を構築します。
- WDK GDL、共用体を構築します。
- WDK GDL、区切り記号を構築します。
- WDK GDL、例を構築します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76133493223329997f5b5cfa0befcc1d4d23870
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581605"
---
# <a name="gdl-constructs"></a>GDL コンストラクト


A *GDL コンストラクト*は単に[GDL 属性](gdl-attributes.md)コンス トラクターの本体が続きます。 論理的には、コンス トラクターを C 構造体と同様、データの収集はかなり表します。

A*本文を構築*、0、1 つ、またはで囲まれた GDL エントリ[区切り文字を構築](gdl-construct-delimiters.md)します。 コンス トラクターの本体は、左中かっこ ({}) で導入され、右中かっこ (}) で終了する必要があります。

構成要素の区切り文字で囲まれた GDL エントリとして参照されます、*内容*コンストラクトの。 囲まれた GDL エントリとも呼ばれます*子*、*子エントリ*、*子要素*、または*メンバー*コンストラクトの。 子エントリでは、構成要素を指定できます。 も、ためには、構造の任意の深さの入れ子を作成することができます。ただし、親の構造の直接の子孫のみを呼び出す*子エントリ*します。

逆に、すぐに子エントリを囲むコンストラクトと呼ばれることはあります、*親コンストラクト*します。 同じ親の構成要素を共有する 2 つの GDL エントリが呼び出される*兄弟*します。 本文に含まれるエントリの親またはエントリの親の親 (とそのために) コンス トラクターが呼び出されます、*先祖コンストラクト*します。

コンス トラクター本体の前にある属性はという名前の*ヘッドを構築*、時折 1、または*構築*します。 コンス トラクターの先頭のキーワードのコンポーネントと呼びます、*型を構築*します。 複数の兄弟の構造が定義されている場合、それぞれ同じ構造型に属していると見なされる、同じキーワードを使用します。 コンス トラクターの先頭の値のコンポーネントと呼びます、*インスタンス名を作成する*、または*タグを構築*します。 構造タグがあると想定されます、[シンボル](gdl-arbitrary-value-contexts.md)します。 構造タグは構文的に省略可能ですが、場合によってが必要です。

構造には、いずれかを指定できる*構文*または*論理*します。 コンストラクトは、共用体で構成できます。

空白および改行シーケンスの任意の大きさが前または後、[区切り文字を構築](gdl-construct-delimiters.md)します。 ただし、読みやすさ、C スタイルのインデントの規則は通常使用されます。

次のコード例では、GDL コンス トラクターを示しています。

```cpp
*ConstructType: ConstructTag
{   *%  Begin Construct Delimiter
*%  this is the Construct Body
*ChildAttribute: child attribute value
*ChildConstruct: ChildConstructTag
{
 *%  Body of Child construct could hold more constructs.
}
*AnotherChildConstruct: ChildConstructTag2
{
 *% Contents of *AnotherChildConstruct
 *% since both child constructs share the same Parent construct, they are
 *% Sibling Constructs.
 *DescendantAttribute:  this attribute is a descendant of  *ConstructType: ConstructTag
}
}   *%  End Construct Delimiter
```

このセクションの内容:

[GDL コンストラクトの区切り記号](gdl-construct-delimiters.md)

[GDL の構文と論理構造](syntactical-and-logical-constructs-in-gdl.md)

[GDL コンストラクトの共用体](gdl-construct-unions.md)

[GDL 空白文字](gdl-whitespace-characters.md)

[GDL コメント](gdl-comments.md)

[GDL 文字列](gdl-strings.md)

 

 




