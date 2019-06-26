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
ms.openlocfilehash: e75da94769aca9ba6a71e49d1494a1e461c90a71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364134"
---
# <a name="c28128"></a>C28128


C28128 を警告します。フィールドへのアクセスが直接行われました。 これは、ルーチンによって行われます。

ドライバーは、特殊な関数を使用してのみアクセスする必要があります構造体のメンバーに直接アクセスします。

たとえば、使用する必要があります、 [ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)を直接変更するのではなく、 **CancelRoutine**のメンバー、 [ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)構造体。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
irp->CancelRoutine = myCancelRoutine;
```

次のコード例は、この警告を回避できます。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

 





