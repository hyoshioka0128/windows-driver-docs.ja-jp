---
title: C28718
description: 警告 C28718 の注釈が付けられていないバッファーです。
ms.assetid: 8417AB73-B645-451D-A359-9A66A793A78D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28718
ms.openlocfilehash: e070adf110ed1a1a5f12c55565f7c9f77b10ebbf
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769724"
---
# <a name="c28718"></a>C28718


警告 C28718: 注釈付きバッファーがありません

この警告は、関数に渡された、または関数によって返されたバッファーが、ソースコード注釈言語 (SAL) の注釈を持っていない場合に報告されます。 静的分析ツールでは、このような注釈を使用してバッファーオーバーランを検出できます。 注釈を追加する方法の詳細については、「 [SAL 注釈を使用した C/c + + コードの欠陥の削減](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)」を参照してください。

現在、この警告を使用して診断されるのは、非定数文字列バッファーのみです。 関数パラメーターとして渡されるすべてのバッファーまたは関数によって返されるすべてのバッファーには、注釈を付けることが理想的です。 **Wchar \_ t**または**char**の配列は、この警告の候補です。 現在、署名されていない文字はありません。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう


次のコード例では、この警告が生成されます。

```
int foo( LPTSTR buffer, size_t cch );  
```

次のコード例では、この警告を回避します。

```
int foo( _Out_writes_(cch) LPTSTR buffer, size_t cch );
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[C/C++ コードの欠陥を減らすための SAL 注釈の使用](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)


 

 






