---
title: C28128
description: 警告 C28128 フィールドへのアクセスが直接行われています。 これはルーチンによって作成される必要があります。
ms.assetid: 66b3345b-fab8-4f1a-b7ab-dfc5e70ca312
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28128
ms.openlocfilehash: 467295590a2e01e59297e412ab9979cf3e7f5841
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839597"
---
# <a name="c28128"></a>C28128


警告 C28128: フィールドへのアクセスが直接行われました。 これはルーチンによって作成される必要があります。

ドライバーは、特殊な関数を使用することによってのみアクセスする必要がある構造体メンバーに直接アクセスしています。

たとえば、 [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)構造体の**cancelルーチン**メンバーを直接変更するのではなく、 [**iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を使用する必要があります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

この警告を elicits するコード例を次に示します。

```
irp->CancelRoutine = myCancelRoutine;
```

次のコード例では、この警告を回避します。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

 





