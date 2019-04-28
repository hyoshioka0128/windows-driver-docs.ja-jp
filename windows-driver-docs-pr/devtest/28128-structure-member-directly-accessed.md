---
title: C28128
description: 警告 C28128 フィールドへのアクセスが直接行われました。 これは、ルーチンによって行われます。
ms.assetid: 66b3345b-fab8-4f1a-b7ab-dfc5e70ca312
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28128
ms.openlocfilehash: 9ad8ed3909536efc44c68a345df069915ebd049b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361410"
---
# <a name="c28128"></a>C28128


C28128 を警告します。フィールドへのアクセスが直接行われました。 これは、ルーチンによって行われます。

ドライバーは、特殊な関数を使用してのみアクセスする必要があります構造体のメンバーに直接アクセスします。

たとえば、使用する必要があります、 [ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)を直接変更するのではなく、 **CancelRoutine**のメンバー、 [ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)構造体。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
irp->CancelRoutine = myCancelRoutine;
```

次のコード例は、この警告を回避できます。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

 





