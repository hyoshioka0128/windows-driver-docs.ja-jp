---
title: その他の GDL マクロ
description: その他の GDL マクロ
ms.assetid: d3c66bc1-815d-484b-b69b-6616d2b43069
keywords:
- GDL WDK、マクロ
- WDK GDL、その他のマクロのマクロ
- IgnoreBlock ディレクティブ WDK GDL
- マクロ WDK GDL、例
- 構造の処理を無効にすると、WDK GDL を構築します。
- WDK GDL を構築します GDL の処理を無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307e3ef168ca7f47488edbc273ceb1c93fa11525
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559395"
---
# <a name="gdl-miscellaneous-macros"></a>その他の GDL マクロ


GDL を使用して、  **\*IgnoreBlock**ディレクティブ、コンストラクトの内容の処理を無効にします。 このディレクティブは、分割し、統治デバッグ戦略を実装する場合に便利ですか、古いコードをコメント アウトします。 内容 **\*IgnoreBlock**引き続きの基本的な構文規則に準拠する必要があります。 無効な GDL または大規模なコメント ブロックは、かっこで囲むことができます&lt;Begin/EndValue:&gt;区切り記号の値を作成し、  **\*IgnoreBlock**します。

次のコード例は、使用する方法を示しています。  **\*IgnoreBlock**します。

```cpp
*IgnoreBlock: <BeginValue:garbage> The code in between does not even need to be valid GDL. }{ " % !!! 
This directive is great for large blocks of comments 
or when you do not want to mark each line with *%  <EndValue:garbage> {}
```

 

 




