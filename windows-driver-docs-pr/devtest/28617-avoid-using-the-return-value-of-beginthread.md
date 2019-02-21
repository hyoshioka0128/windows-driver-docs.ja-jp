---
title: C28617
description: 警告 C28617 では、_beginthread() の戻り値を使用しないでください。 代わりにします。
ms.assetid: b0de0809-1583-4c1d-ad70-c3e27afc3e6d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28617
ms.openlocfilehash: c47ab4d9199c1f1def1d76a4172c91dca9d0bc14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553468"
---
# <a name="c28617"></a>C28617


C28617 を警告します。戻り値を使用しないように\_beginthread() します。 使用\_beginthreadex() 代わりに

使用する方が安全 **\_beginthreadex**より **\_beginthread**します。 場合により、スレッドが生成された **\_beginthread**の呼び出し元に返されるハンドルを迅速に終了 **\_beginthread**無効か、悪い、別のスレッドを指す可能性があります。 ただし、によって、ハンドルが返されます **\_beginthreadex**の呼び出し元によって閉じられますが、  **\_beginthreadex**ので、有効なハンドルである場合は必ず **\_beginthreadex**エラーが返されませんでした。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次のコード例では、この警告を生成します。

```
hThread = (HANDLE)_beginthread (&SecondThreadFunc, 0, &args);
WaitForSingleObject (hThread, INFINITE);
```

次のコード例は、警告を回避できます。

```
hThread = (HANDLE)_beginthreadex ( NULL, 0,
                                   &SecondThreadFunc,
                                   &args, 0, &threadID);
WaitForSingleObject (hThread, INFINITE);
CloseHandle(hThread);
```

 

 





