---
title: GDL コンストラクト区切り記号
description: GDL コンストラクト区切り記号
ms.assetid: 6f759534-3dc2-4e04-afe0-3f377790be21
keywords:
- WDK GDL、区切り記号を構築します。
- GDL の WDK を構築します
- パーサー WDK GDL、コンストラクトの区切り記号の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93560efa1e0ba3ac3c92f4ce533d9545ac230f48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574369"
---
# <a name="gdl-construct-delimiters"></a>GDL コンストラクト区切り記号


*区切り記号を構築*文字は、中かっこ: {および}。 従うか、linebreak シーケンスを持つコンス トラクターの区切り記号の前にする必要がありますので、linebreak と同様にコンストラクトの区切り記号の文字さらに動作します。

次の 2 つのコード例では、コンス トラクターの区切り記号の使用を示します。 最初の例では、複数の行にまたがる値を持ちます。

```cpp
*Person: FlorenceF
{
 *Company:Contoso Pharmaceuticals
 {
 *Location: Redmond, WA
 }
}
```

2 番目の例は 1 行に値を結合を値の部分を区切るために、中かっこを使用します。

```cpp
*Person: FlorenceF{*Company:Contoso Pharmaceuticals{*Location: Redmond, WA}}
```

 

 




