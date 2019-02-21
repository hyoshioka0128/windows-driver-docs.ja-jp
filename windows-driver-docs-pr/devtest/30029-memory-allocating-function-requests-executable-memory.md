---
title: C30029
description: 警告 C30029 がメモリの割り当て関数を呼び出す実行可能なメモリを要求します。
ms.assetid: E32E6EDB-010A-4E7F-8505-1E7557BB3FDF
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30029
ms.openlocfilehash: 0b1b9772cffc84738135cc75701ddab148492b26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558173"
---
# <a name="c30029"></a>C30029


C30029 を警告します。メモリの割り当てを実行可能なメモリを要求する関数を呼び出す

禁止\_MEM\_割り当て\_単純に-NOTYPE

一部の Api は、実行可能ファイルの非ページ プールのみを割り当てます。 この動作を変更することを指定するパラメーターはありません。 この問題を解決する唯一の方法では、代替の非実行可能ファイルの非ページ プール メモリの割り当てを許可する API を使用します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコードでは、警告 C30029 が生成されます。

```
MmMapIoSpace(  PhysicalAddress,
        numberOfBytes,
        PAGE_NOCACHE);
```

次のコードは、この警告を回避できます。

```
MmMapIoSpaceEx(    PhysicalAddress,
        numberOfBytes,
        PAGE_NOCACHE | PAGE_READWRITE);
```

 

 





