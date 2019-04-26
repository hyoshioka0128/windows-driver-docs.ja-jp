---
title: GDL コンストラクト ユニオン
description: GDL コンストラクト ユニオン
ms.assetid: 0ca237fe-7f47-4b9c-8963-676a2afd1140
keywords:
- WDK GDL、共用体を構築します。
- WDK GDL の論理構造
- WDK GDL、論理構造を構築します。
- WDK GDL、例を構築します。
- 兄弟は、WDK GDL を構築します。
- WDK GDL 共用体
- パーサー WDK GDL、共用体の処理
- GDL WDK、共用体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d657e3fbb9bc98a70d394d2bd25b0cc55a89bd5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342200"
---
# <a name="gdl-construct-unions"></a>GDL コンストラクト ユニオン


複数の構成要素と同じ型を構築して、構造タグ、GDL ソースで定義されている場合のファイル、その構成要素の論理表現 (、[の論理コンストラクト](syntactical-and-logical-constructs-in-gdl.md)) は、元のコンテンツの共用体が含まれますGDL ソース ファイルで定義されている構成要素。

構造型と構造タグをまとめて一意に指定か、(その親のコンテキスト) 内の論理コンストラクトを定義します。 2 つの XML とは異なり*兄弟*構造が定義されている、同じ構造型と構造タグ、結果が 1 つの論理コンストラクトです。 実際には、コンストラクトは、構文の兄弟になるために必要はありません、論理兄弟になることができます。 (*構文兄弟*明示的に同じのコンス トラクター本体に存在し、*論理兄弟*同じ論理構造の両方の子である)。

論理構造の内容は、兄弟の内容の和集合です。 論理構造の構成要素ではありませんは GDL ソース ファイルで構文的に定義されていたはスナップショットに表示される内容です。 次のコード例では、2 つの兄弟構造が構築型の両方があります。\*Person コンストラクトのタグを使用して。FlorenceF します。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
}
}
*Person: FlorenceF
{
*Position: CEO
*Company:Contoso Pharmaceuticals
{
*NumberOfEmployees: 43,000
}
}
```

上記の規則に従って 2 つの兄弟が両方の兄弟の和集合を含む 1 つの論理コンストラクトを定義します。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
}
*Position: CEO
*Company:Contoso Pharmaceuticals
{
*NumberOfEmployees: 43,000
}
}
```

前の例でマージが同じ構築型を持つ 2 つの新しい兄弟構造を作成したことに注意してください。\*会社とコンストラクト タグ:Contoso Pharmaceuticals します。

同じ規則が適用された場合は、もう一度 (再帰) は、次のコードになります。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
*NumberOfEmployees: 43,000
}
*Position: CEO
}
```

これらが解析されるときの前の 3 つ GDL フラグメントのいずれかには、同じ内部表現が生成されます。 内部表現には、最後のフラグメントが最も近いに似ています。

ときに[属性](gdl-attributes.md)同じ[キーワード](gdl-keywords.md)乗算が定義されている場合、マージは行われません。 各定義は、内部表現に引き続き存在します。 Template ディレクティブ**\*加法**スナップショットに転送はどのような値または値を指定するために使用します。

GDL パーサーは、GDL ストリームの構文形式を受け取り、GDL コマンドの内部の論理表現を作成します。 これらのコマンドの内部表現は、XML に変換され、スナップショットになります。

 

 




