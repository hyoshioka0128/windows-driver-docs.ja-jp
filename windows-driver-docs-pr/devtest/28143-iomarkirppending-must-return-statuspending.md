---
title: C28143
description: 警告 C28143 IoMarkIrpPending を呼び出すディスパッチルーチンもありますを返す必要があります。
ms.assetid: 3b9e6c4f-73d1-4abc-9495-85bb56e2532b
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28143
ms.openlocfilehash: a78c01d225402b89f66dcc3c8557c4bdc0a4f525
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840315"
---
# <a name="c28143"></a>C28143


警告 C28143: IoMarkIrpPending を呼び出すディスパッチルーチンは、状態\_保留中にも返す必要があります

[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出すディスパッチルーチンには、ドライバーがステータス\_PENDING 以外の値を返すパスが少なくとも1つ含まれています。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

この警告を elicits するコード例を次に示します。

```
IoMarkIrpPending(Irp);
...
return STATUS_SUCCESS;
```

次のコード例では、この警告を回避します。

```
IoMarkIrpPending(Irp);
...
return STATUS_PENDING;
```

 

 





