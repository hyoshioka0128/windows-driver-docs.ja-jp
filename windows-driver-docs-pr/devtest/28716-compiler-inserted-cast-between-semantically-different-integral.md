---
title: C28716
description: C28716 コンパイラ挿入されたキャスト意味の異なる整数型の間に警告します。
ms.assetid: 6cb5e57f-3535-4ef2-b586-d46d0de60a4b
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28716
ms.openlocfilehash: 31b8751ef4f1a130c13870ef71456a3ff5b6ec67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577695"
---
# <a name="c28716"></a>C28716


C28716 を警告します。意味の異なる整数型の間のキャストのコンパイラ挿入されました。

この警告は、ブール値として使用されていることを示します、 **NTSTATUS**せず、明示的にキャストします。 これは、結果が望ましくない可能性があります。 ブール値 (false) を返す関数の一般的な障害の値としてテストされたときに、成功状態を示しますたとえば、 **NTSTATUS**します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

PREfast では、次の例では、警告を報告します。

```
extern bool SomeMemAllocFunction(void **);

return SomeMemAllocFunction(&MyPtr);
```

次の例では、このエラーを回避します。

```
extern bool SomeMemAllocFunction(void **);

if (SomeMemAllocFunction(&MyPtr) == true) {
 return STATUS_SUCCESS;
} else {
 return STATUS_NO_MEMORY;
}
```

 

 





