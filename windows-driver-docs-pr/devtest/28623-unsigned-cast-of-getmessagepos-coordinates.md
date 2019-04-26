---
title: C28623
description: GetMessagePos() の座標の C28623 符号なしのキャストを警告します。 Loword マクロと HIWORD ではなく、処理するように/GET_Y_LPARAM を使用します。
ms.assetid: 155da4f5-4e77-451e-b26b-69a39c32effa
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28623
ms.openlocfilehash: bb3c2190439e84f27557a4cdea2353ab5bcb7400
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347153"
---
# <a name="c28623"></a>C28623


C28623 を警告します。座標の GetMessagePos() の符号なしのキャスト。 GET を使用して、\_X\_LPARAM/取得\_Y\_loword マクロと HIWORD ではなく LPARAM

複数のモニターでシステムには、負の x 座標と y 座標を持つことができます。 このようなシステムでは、 **GetMessagePos**負の値を返すため可能性があります。 ただし、ため**LOWORD**と**HIWORD**として符号なし数量の座標を扱う、それらは使用できません。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

PREfast では、次の例では、警告を報告します。

```
DWORD dw = GetMessagePos();
POINT ppt;

ppt.x = LOWORD(dw);
ppt.y = HIWORD(dw);
```

次の例では、このエラーを回避します。

```
DWORD dw = GetMessagePos();
POINT ppt;

ppt.x = GET_X_LPARAM(dw);
ppt.y = GET_Y_LPARAM(dw);
```

 

 





