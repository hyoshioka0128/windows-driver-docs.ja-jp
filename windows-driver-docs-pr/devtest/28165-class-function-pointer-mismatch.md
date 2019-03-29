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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572393"
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

 

 





