---
title: C28723
description: 対応する宣言がない関数定義で警告 C28723 Unannotated バッファー。
ms.assetid: FE481A48-F4C1-4C25-8CE6-3802D57B8F68
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28723
ms.openlocfilehash: 00ab9831c34b4aed7f7ec81c31fa67cdab60402a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535390"
---
# <a name="c28723"></a>C28723


C28723 を警告します。対応する宣言がない関数定義で unannotated バッファー

この警告は、Microsoft ソース コード注釈言語 (SAL) を関数パラメーターとして渡されるか、関数によって返されるバッファーに注釈を付けることを示します。 静的分析ツールでは、バッファー オーバーランを検出するために、このような注釈を使用できます。

現時点では、この警告を非定数バッファーにのみが診断します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```
    int foo( LPTSTR buffer, size_t cch )
{
    ...
}  
```

次のコード例は、この警告を回避できます。

```
    int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch )
{
    ...
}
```









