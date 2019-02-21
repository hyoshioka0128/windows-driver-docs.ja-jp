---
title: C28742
description: 関数で警告 C28742 Unannotated バッファー。
ms.assetid: 04B2D637-360F-4347-8533-FEDC81FCE40D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28742
ms.openlocfilehash: bf950cb61996e763f36b4551cdf439ff9b4a9f6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528000"
---
# <a name="c28742"></a>C28742


C28742 を警告します。関数で unannotated バッファー

この警告は、Microsoft ソース コード注釈言語 (SAL) を関数パラメーターとして渡されるか、関数によって返されるバッファーに注釈を付けることを示します。 静的分析ツールでは、バッファー オーバーランを検出するために、このような注釈を使用できます。

現時点では、この警告を非定数バッファーにのみが診断します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```
       int foo( LPTSTR buffer, size_t cch );
```

次のコード例では、この警告を回避 SAL 注釈を使用して**\_アウト\_書き込みます\_** 呼び出された関数がバッファーに書き出すことと、バッファーが NULL にすることはできませんを指定します。 注釈は、のバッファーがあることを示します*cch*要素。

```
       int foo(_Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





