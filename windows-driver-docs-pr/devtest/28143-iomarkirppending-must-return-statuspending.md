---
title: C28143
description: IoMarkIrpPending を呼び出す警告 C28143 A ディスパッチ ルーチンは STATUS_PENDING を返すもする必要があります。
ms.assetid: 3b9e6c4f-73d1-4abc-9495-85bb56e2532b
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28143
ms.openlocfilehash: 8ceebf56e2341a885d11d11416ecc4c2e748259a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361584"
---
# <a name="c28143"></a>C28143


C28143 を警告します。IoMarkIrpPending を呼び出すディスパッチ ルーチンは、状態を返す必要がありますも\_PENDING

呼び出すディスパッチ ルーチン[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)ドライバーが状態以外の値を返すに少なくとも 1 つのパスを含む\_保留します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
IoMarkIrpPending(Irp);
...
return STATUS_SUCCESS;
```

次のコード例は、この警告を回避できます。

```
IoMarkIrpPending(Irp);
...
return STATUS_PENDING;
```

 

 





