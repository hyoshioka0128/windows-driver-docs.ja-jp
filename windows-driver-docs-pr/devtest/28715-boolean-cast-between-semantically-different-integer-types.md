---
title: C28715
description: 意味の異なる整数型の間の警告 C28715 キャストします。
ms.assetid: 49e37718-9950-4f63-a554-f924ae8cf0a4
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28715
ms.openlocfilehash: fb82a420c90e0788473346af266a19088adad86b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570829"
---
# <a name="c28715"></a>C28715


C28715 を警告します。意味の異なる整数型の間のキャストします。

この警告は、ブール値にキャストされることを示します**NTSTATUS**します。 これは、結果が望ましくない可能性があります。 たとえば、一般的な障害値をブール値を返す関数の (**FALSE**) としてテストされたときに、成功の状態は、 **NTSTATUS**。

通常、ブール値を返す関数がいずれか 1 を返します (の**TRUE**) または 0 (の**FALSE**)。 2 つの値は、成功コードとして扱われます、 **NT\_成功**マクロ。 したがって、障害の場合は検出されることはありません。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

PREfast では、次の例では、警告を報告します。

```
extern BOOL SomeFunction(void);

if (NT_SUCCESS(SomeFunction())) {
   return 0;
} else {
   return -1;
}
```

次の例では、このエラーを回避します。

```
extern BOOL SomeFunction(void);

if (SomeFunction() == TRUE) {
   return 0;
} else {
   return -1;
}
```

 

 





