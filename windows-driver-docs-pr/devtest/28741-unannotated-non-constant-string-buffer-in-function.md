---
title: C28741
description: 関数で警告 C28741 Unannotated バッファー。
ms.assetid: 85F071C2-C91B-43D6-8F59-F1D1F955ECC1
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28741
ms.openlocfilehash: c8d4c02623eebce83909f33fd51d2375132886b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374732"
---
# <a name="c28741"></a>C28741


C28741 を警告します。関数で unannotated バッファー

この警告は、Microsoft ソース コード注釈言語 (SAL) を関数パラメーターとして渡されるか、関数によって返されるバッファーに注釈を付けることを示します。 静的分析ツールでは、バッファー オーバーランを検出するために、このような注釈を使用できます。

現時点では、この警告を非定数の文字列バッファーにのみが診断します。 理想的には、関数のパラメーターとして渡されたか、関数によって返されるすべてのバッファーを注釈する必要があります。 配列の**wchar\_t**または**char**この警告の候補となります。 符号なし文字現在はできません。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次の例のコードには、この警告が生成されます。

```
  int foo( LPTSTR buffer, size_t cch );
```

次のコード例では、この警告を回避 SAL 注釈を使用して**\_アウト\_書き込みます\_** 呼び出された関数がバッファーに書き出すことと、バッファーが NULL にすることはできませんを指定します。 注釈は、のバッファーがあることを示します*cch*要素。

```
    int foo(_Out_writes_(cch) LPTSTR buffer, size_t cch );
```

 

 





