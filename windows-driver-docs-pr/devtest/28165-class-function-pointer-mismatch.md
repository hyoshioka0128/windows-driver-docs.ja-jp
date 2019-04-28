---
title: C28165
description: 警告 C28165 クラスの関数ポインターが関数クラスと一致しません。
ms.assetid: 0fc2b542-058c-4e98-b08e-2661c65e2dd0
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28165
ms.openlocfilehash: dd74ec126a3ac5a3a51c527acbcc34c09fb34558
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361336"
---
# <a name="c28165"></a>C28165


C28165 を警告します。クラスの関数ポインターが関数クラスと一致しません

関数ポインターが、  **\_ \_drv\_functionClass**注釈には特定の機能のクラスの関数のみを割り当てる必要がありますを指定します。 割り当てまたは関数呼び出しで暗黙の割り当てでは、ソースとターゲットを同じ関数のクラスにある必要がありますが、関数クラスが一致しません。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
IoSetCancelRoutine(MyStartIo);
```

次のコード例は、この警告を回避できます。

```
IoSetCancelRoutine(MyCancelRoutine);
```

 

 





