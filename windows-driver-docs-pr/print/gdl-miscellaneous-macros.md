---
title: GDL その他のマクロ
description: GDL その他のマクロ
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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338361"
---
# <a name="gdl-miscellaneous-macros"></a>GDL その他のマクロ


GDL を使用して、  **\*IgnoreBlock**ディレクティブ、コンストラクトの内容の処理を無効にします。 このディレクティブは、分割し、統治デバッグ戦略を実装する場合に便利ですか、古いコードをコメント アウトします。 内容 **\*IgnoreBlock**引き続きの基本的な構文規則に準拠する必要があります。 無効な GDL または大規模なコメント ブロックは、かっこで囲むことができます&lt;Begin/EndValue:&gt;区切り記号の値を作成し、  **\*IgnoreBlock**します。

次のコード例は、使用する方法を示しています。  **\*IgnoreBlock**します。

```cpp
*IgnoreBlock: <BeginValue:garbage> The code in between does not even need to be valid GDL. }{ " % !!! 
This directive is great for large blocks of comments 
or when you do not want to mark each line with *%  <EndValue:garbage> {}
```

 

 




