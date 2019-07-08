---
title: C28722
description: 関数宣言で C28722 Unannotated バッファーを警告します。
ms.assetid: 460B9F71-9878-4DC8-8B93-6DCDF1544213
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28722
ms.openlocfilehash: 8624b4e1ed7e5b72714864546d4fcf9aa99c2ae2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363860"
---
# <a name="c28722"></a>C28722


C28722 を警告します。関数宣言で unannotated バッファー

この警告は、Microsoft ソース コード注釈言語 (SAL) を関数パラメーターとして渡されるか、関数によって返されるバッファーに注釈を付けることを示します。 静的分析ツールでは、コンパイル時にバッファー オーバーランを検出するために、このような注釈を使用できます。

現時点では、この警告を非定数バッファーにのみが診断します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```CSS
int foo( LPTSTR buffer, size_t cch );  
```

次のコード例では、この警告を回避 SAL 注釈を使用して **\_アウト\_書き込みます\_** 呼び出された関数がバッファーに書き出すことと、バッファーが NULL にすることはできませんを指定します。 注釈は、のバッファーがあることを示します*cch*要素。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





