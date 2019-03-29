---
title: C28652
description: 警告 C28652 静的初期化子では、オーバー ロードされたビット処理演算子のための書き込みページ上のコピーが行われます。
ms.assetid: 763A7F2E-ABFF-41D2-9077-4F60B8EBD338
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28652
ms.openlocfilehash: 980e92fd2e250ea745a8b1f543614690e25ecf54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579179"
---
# <a name="c28652"></a>C28652


C28652 を警告します。静的初期化子がオーバー ロードされたビット処理演算子のための書き込みページでコピーを原因します。

グローバルまたは静的の const 変数の静的初期化子は、コンパイル時に多くの場合、完全に評価することができ、ため、.rdata のセクションで生成することができます。 ただし、任意の初期化子は、関数呼び出しを必要とする場合、全体の初期化子可能性がありますに配置するコピー オン ライトのページ コスト パフォーマンスを持ちます。 この初期化は、列挙型でオーバー ロードされたビット処理演算子への呼び出しが。 場合は、オーバー ロードを実装では、明確なセマンティクスを持つ、適切なキャストまたはマクロを使用すると、同じ効果がコピー オン ライトを必要とせず生成できます。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```
#include <nt.h>

typedef enum
{
    ENUM_VAL_1 = 0x1,
    ENUM_VAL_2 = 0x2,
    ENUM_VAL_3 = 0x4
} ENUM_VALS;

DEFINE_ENUM_FLAG_OPERATORS(ENUM_VALS);

const ENUM_VALS rgValsRuntime[] = {
    ENUM_VAL_1 | ENUM_VAL_2,    // Runtime init!
    ENUM_VAL_3                  // Compile time init
};  
```

次のコード例は、この警告を回避できます。

```
#include <nt.h>

typedef enum
{
    ENUM_VAL_1 = 0x1,
    ENUM_VAL_2 = 0x2,
    ENUM_VAL_3 = 0x4
} ENUM_VALS;

DEFINE_ENUM_FLAG_OPERATORS(ENUM_VALS);

const ENUM_VALS rgValsRuntime[] = {
    (ENUM_VALS) COMPILETIME_OR_2FLAGS(ENUM_VAL_1, ENUM_VAL_2),
    ENUM_VAL_3                  // Compile time init
};
```









