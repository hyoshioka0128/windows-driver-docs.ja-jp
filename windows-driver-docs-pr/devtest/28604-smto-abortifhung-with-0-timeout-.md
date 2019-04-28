---
title: C28604
description: C28604 Sendmessagetimeout を SMTO_ABORTIFHUNG 0 のタイムアウト警告。
ms.assetid: d9be9747-20f6-4a2b-a841-eaf3255f2f65
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28604
ms.openlocfilehash: 15a702c26f1f54b9ee7d8cff14e93136095f2c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376772"
---
# <a name="c28604"></a>C28604


C28604 を警告します。Sendmessagetimeout SMTO を\_ABORTIFHUNG 0 のタイムアウトで

コード分析ツールは、アプリケーションを呼び出すときに、この警告を報告**SendMessageTimeout**で、 **SMTO\_ABORTIFHUNG**フラグと、0 のタイムアウト期間。 使用して**SendMessageTimeout**タイムアウト期間には、効果がなく、呼び出しはブロッキング呼び出しとして扱われますので、この方法は問題が発生することができます。

タイムアウト期間を 0 以外の値を指定します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の関数呼び出しには、プロセスを無期限に応答していない可能性があります。

```
fNeedsCallbackEvent = (0 != SendMessageTimeout(
_hwnd, 
WM_NULL, 
0,
0, 
SMTO_ABORTIFHUNG,
0,
&dwResult)); 
```

次の関数呼び出しには、この問題はありません。

```
fNeedsCallbackEvent = (0 != SendMessageTimeout(
_hwnd, 
WM_NULL, 
0,
0,
SMTO_ABORTIFHUNG,
1000,  
&dwResult)); 
```

 

 





