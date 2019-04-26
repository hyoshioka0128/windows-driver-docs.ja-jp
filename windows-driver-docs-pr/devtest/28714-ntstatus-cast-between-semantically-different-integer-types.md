---
title: C28714
description: 意味の異なる整数型の間の警告 C28714 キャストします。
ms.assetid: 53acc1a1-58a9-4009-a15c-2b11f31b086d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28714
ms.openlocfilehash: 977ae0125efd1a82f872367ed5335311b477ac62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345864"
---
# <a name="c28714"></a>C28714


C28714 を警告します。意味の異なる整数型の間のキャストします。

この警告では、ことを示します、 **NTSTATUS**値がブール型に明示的にキャストされています。 これは、結果が望ましくない可能性があります。 などの一般的な成功値**NTSTATUS**、**状態\_成功**は**false**ブール値としてテストするとします。

ほとんどの場合、 **NT\_成功**マクロは、の値をテストするために使用する必要があります、 **NTSTATUS**します。 このマクロを返します**true**返される状態値が、警告もエラー コードの場合。 関数がその障害/成功を示すブール値を返す場合にする必要があります明示的に適切なブール型を返すではなくのキャストに依存して**NTSTATUS**ブール型にします。

また、場合によってはプログラムを試みる可能性がありますブール値を格納するローカル変数を再利用**NTSTATUS**値。 この方法は、エラーが発生しやすい; は多くの場合、方がはるかに安全です (可能性があるとより効率的な) を使用して、個別の**NTSTATUS**変数。

 

 





