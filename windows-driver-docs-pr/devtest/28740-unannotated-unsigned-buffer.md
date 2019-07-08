---
title: C28740
description: 警告 C28740 Unannotated 符号なしのバッファー。
ms.assetid: 849BA4E4-89E7-4E8C-B73C-CA303487A5E3
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28740
ms.openlocfilehash: 83530c43b283d4e54291c01f7e98ba89d536be66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374740"
---
# <a name="c28740"></a>C28740


C28740 を警告します。Unannotated 符号なしのバッファー

この警告は、Microsoft ソース コード注釈言語 (SAL) を関数パラメーターとして渡されるか、関数によって返されるバッファーに注釈を付けることを示します。 静的分析ツールでは、バッファー オーバーランを検出するために、このような注釈を使用できます。

現時点では、この警告を非定数バッファーにのみが診断します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```
    int foo( BYTE * buffer, size_t cch ); 
```

次のコード例では、この警告を回避 SAL 注釈を使用して **\_アウト\_書き込みます\_** 呼び出された関数がバッファーに書き出すことと、バッファーが NULL にすることはできませんを指定します。 注釈は、のバッファーがあることを示します*cch*要素。

```
    int foo( _Out_writes_(cch) BYTE * buffer, size_t cch );
```

 

 





