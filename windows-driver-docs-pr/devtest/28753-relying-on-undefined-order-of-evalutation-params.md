---
title: C28753
description: パラメーターの評価の順序は定義上 C28753 証明書利用者を警告します。
ms.assetid: D8879714-63A2-4F36-B08A-1E487ACB5BC1
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28753
ms.openlocfilehash: f95dcececc7071227dec9f761f0f5af9f2873100
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559773"
---
# <a name="c28753"></a>C28753


C28753 を警告します。未定義のパラメーターの評価順序に依存

C と C++ では任意の順序で指定された実引数を評価するコードを生成するコンパイラおよび x86 と ARM コンパイラが異なる順序を選択する傾向があります。 特定の順序に依存するコードは、さまざまなプラットフォームで動作が異なる場合があります。

よくある間違いは、スマート ポインターの使用には、address-of 演算子**&** 副作用が、このような呼び出し。

```ManagedCPlusPlus
sp->Foo(&sp);
```

メンバー アクセス演算子への呼び出し**- &gt;** と演算子**&** 任意の順序で発生する可能性があります。 したがって副作用演算子から**&** 演算子の前後に発生する可能性があります**- &gt;** が呼び出されます。 この警告は、プラットフォーム間で異なる動作を防ぐためにこれらのバグのある呼び出しを検索します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次の例のコードには、この警告が生成されます。

```ManagedCPlusPlus
sp->Foo(&sp)
```

次のコード例は、この警告を回避できます。

```ManagedCPlusPlus
SmartPtr spTemp;
sp->Foo(&spTemp);
sp = spTemp;
```

 

 





