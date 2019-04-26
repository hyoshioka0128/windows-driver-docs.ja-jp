---
title: C28718
description: 警告 C28718 Unannotated バッファー。
ms.assetid: 8417AB73-B645-451D-A359-9A66A793A78D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28718
ms.openlocfilehash: cd4afb516ac9df4d2d9a92116f59c3569ae3c5cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345852"
---
# <a name="c28718"></a>C28718


C28718 を警告します。Unannotated バッファー

この警告は、関数に渡されるか、関数によって返されるバッファーにソース コード注釈言語 (SAL) の注釈があるない場合に報告されます。 静的分析ツールでは、バッファー オーバーランを検出するために、このような注釈を使用できます。 注釈を追加する方法の詳細については、次を参照してください。 [C と C++ コードの欠陥を削減する SAL 注釈を使って](https://go.microsoft.com/fwlink/p/?linkid=247283)と**に注釈を付ける関数のパラメーターと戻り値**します。

現時点では、この警告を非定数の文字列バッファーにのみが診断します。 理想的には、関数のパラメーターとして渡されたか、関数によって返されるすべてのバッファーを注釈する必要があります。 配列の**wchar\_t**または**char**この警告の候補となります。 符号なし文字現在はできません。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、この警告を生成します。

```
int foo( LPTSTR buffer, size_t cch );  
```

次のコード例は、この警告を回避できます。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[C/C++ コードの欠陥を減らすための SAL 注釈の使用](https://go.microsoft.com/fwlink/p/?linkid=247283)

**関数パラメーターおよび戻り値の注釈設定**
 

 






