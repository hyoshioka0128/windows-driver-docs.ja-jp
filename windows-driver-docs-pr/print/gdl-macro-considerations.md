---
title: GDL マクロ考慮事項
description: GDL マクロ考慮事項
ms.assetid: b1e3e32f-2f5f-47ae-b69b-7645ada59c2a
keywords:
- GDL WDK、マクロ
- マクロ WDK GDL、考慮事項
- WDK を参照渡す GDL マクロ
- マクロ WDK GDL、渡すマクロ参照します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a249c243574095846b55ee3f0e9022f27a9aa6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353118"
---
# <a name="gdl-macro-considerations"></a>GDL マクロ考慮事項


GDL マクロは、スコープと有効期間があります。 マクロは、マクロ定義のコンス トラクターを含む入れ子のレベルが終わるまで定義のポイントからのみ参照できます。

ルート レベルで定義されているマクロは無制限のスコープと有効期間。 同じ名前の複数のマクロは、同じ名前空間で定義できます。 最新の定義には、任意の以前の定義が非表示にします。 最上位の定義に有効期限が切れた後に前の定義が対象になります。

ブロックのマクロ定義で使用する場合、  **\#Includes**プリコンパイル済みファイルをインクルードするディレクティブ、ファイルの内容は表示されませんマクロ定義内でないは、プリコンパイル済みとして宣言されているファイルで行を使用するため、スタンドアロン エンティティになります。

旧バージョンと互換性のため、値のすべてのマクロ定義のパラメーターの値のサポートが有効にします。

マクロ定義には、それ自体を参照できません。 ただし、マクロの参照では、パラメーターとして自体への参照を渡すことができます。

次のコード例では、参照を渡す方法を示します。

```cpp
*InsertBlock:  Myself(Myself(AnotherMacro))
```

 

 




